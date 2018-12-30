---
layout: post
title: "[CTF]35C3 Junior CTF McDonald"
date: 2018-12-31 00:25:20 +0800
categories: [web,security,CTF]
tags: [web,security,CTF]
---


## 題目名稱:McDonald

### 題目網址:http://35.207.132.47:85/



Our web admin name's "Mc Donald" and he likes apples and always forgets to throw away his apple cores..

打開網頁會看到

![1](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2018-12-31/1.png)

什麼按鈕都沒有，查看robots.txt
<br />
發現 禁止google爬取 /backup/.DS_Store

![2](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2018-12-31/2.png)

**重點在於.DS_Store**
```
.DS_Store 是一種由蘋果公司的Mac OS X作業系統所創造的隱藏文件，目的在於存貯目錄的自定義屬性，例如文件們的圖標位置或者是背景色的選擇。
```

這邊使用
`ds_store_exp工具`
[https://github.com/lijiejie/ds_store_exp](https://github.com/lijiejie/ds_store_exp)

.DS_Store工具 將文件遞歸下載


答案最後在/backup/b/a/c/flag.txt



回網頁讀取 
```
http://35.207.132.47:85/backup/b/a/c/flag.txt
```
也會有一樣答案


