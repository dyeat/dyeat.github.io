---
layout: post
title: "[逆向]Ollydbg-patch"
date: 2018-12-21 23:22:02 +0800
categories: [reverse]
tags: [reverse]
---

### 利用patch使驗證失效

這次範例<br />
![1.png](https://dyeat.github.io/static/img/2018-12-21/2.png)

先亂輸入用戶名與序號列 點擊Check <br />
![2.png](https://dyeat.github.io/static/img/2018-12-21/1.png)


會得到錯誤訊息

丟進Ollydbg  開始跟進 找斷點
 ![3.png](https://dyeat.github.io/static/img/2018-12-21/3.png)
 <br />

在`004011B4`與`004011C8`這邊發現`GetDlgItemTextA`

`004011D2  CMP EBX,5   //可以推算 用戶名 大概是五個字元`

重點在`004011F5`這句 

`004011F5  JE SHORT TrackMe.0040122E`

意思大概就是 
```C=
if ( x <= 5)
	printf("驗證成功!"\n");
else
	printf("驗證錯誤!"\n");
```
    
  只要`004011F5`一句不跳轉即可註冊成功
  
 `在這把004011F5改成NOP`
  
![4.png](https://dyeat.github.io/static/img/2018-12-21/4.png)
  
  再另外新生成一個檔案
  
  
  這時候輸入的任何字元 都是認證成功
  
![5.png](https://dyeat.github.io/static/img/2018-12-21/5.png)
