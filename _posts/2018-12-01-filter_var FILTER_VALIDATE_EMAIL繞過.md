---
layout: post
title: "[PHP] filter_var FILTER_VALIDATE_EMAIL 繞過"
date: 2018-12-01 21:20:00 +0800
categories: [php, security]
tags: [php, security]
---

### [資料來源](https://tricking.io/card/14/content)


filter_var是一組PHP中過濾、檢測用戶輸入的方法，其中開發者通常利用filter_var($email, FILTER_VALIDATE_EMAIL)來過濾用戶輸入的信箱。

RFC 3696規定信箱local part部分可以用雙引號包裹，雙引號內即可填入任意字符。

我們可以利用RFC 3696，傳入"aaa'aaa"@example.com，即可保留單引號，並通過filter_var的檢測，最終觸發SQL注入漏洞。


這個點早在當初PHPMailer的`CVE-2016-10033`提到過。

RFC 3696規定，信箱地址分為local part和domain part兩部分。 local part中包含特殊字符，需要如下處理：

將特殊字符用\轉義，如`Joe\'Blow@example.com`
或將local part包裹在雙引號中，如`"Joe'Blow"@example.com`
local part長度不超過64個字符
雖然PHP沒有完全按照RFC 3696進行檢測，但支持上述第2種寫法。所以，我們可以利用之繞過`FILTER_VALIDATE_EMAIL`的檢測。

因為程式碼中信箱是用戶名、@、Host三者拼接而成，但用戶名是經過了轉義的，所以單引號只能放在Host中。我們可以傳入信箱為`"aaa'"@example.com。 `

這個信箱是合法的：

```php
<?php

$email = '"@aaa\'"@example.com';

var_dump(filter_var($email, FILTER_VALIDATE_EMAIL));
```

這個信箱包含單引號，將閉合SQL語句中原本的單引號，造成SQL注入漏洞。


以下為程式碼
---
```php
<?php
function actionRegister()
{
    if ( $_POST ) {
        $username = arg('username');
        $password = arg('password');

        if ( empty($username) || empty($password) )
        {
            $this->error('Username or password is empty.');
        }

        $email = arg('email');
        if ( empty($email) )
        {
            $email = $username . '@' . arg('HTTP_HOST');
        }

        if ( !filter_var($email, FILTER_VALIDATE_EMAIL) )
        {
            $this->error('Email error.');
        }

        $user = new User();
        $data = $user->query("SELECT * FROM `{$user->table_name}` WHERE `username` = '{$username}'");

        if ($data)
        {
            $this->error('This username is exists.');
        }

        $ret = $user->create([
            'username' => $username,
            'password' => md5($password),
            'email' => $email
        ]);

        if ($ret)
        {
            $_SESSION['user_id'] = $user->lastInsertId();
        }
        else
        {
            $this->error('Unknown error.');
        }
    }

}
```
