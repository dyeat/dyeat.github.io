---
layout: post                          
title: "Linux 設定$PATH路徑環境變數"
date: 2019-1-21 22:37:00 +0800       
categories: [linux]         
tags: [linux]                     
---

查看目前環境變數


```sh
echo $PATH
```

會輸出類似這樣的內容：

```sh
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin
```

自訂目錄路徑到 $PATH 環境變數：


```sh
$ vim ~/.bash_profile
```

```sh
$ export PATH=$PATH:[路徑]
```

存檔後執行

```sh
$ source ~/.bash_profile
```

再次輸出查看
```sh
echo $PATH
```


