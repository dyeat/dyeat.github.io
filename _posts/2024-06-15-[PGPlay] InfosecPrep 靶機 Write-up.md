---
layout: post
title: "[PGPlay] InfosecPrep 靶機 Write-up"
date: 2024-06-15 22:50:02 +0800
categories: [offsec]
tags: [offsec]
---

本系列為 Proving Grounds Play Free 靶機

官方難度 : Easy

社群認定難度 : Easy

知識點 : openssh key 權限必須為 600

### port Scan

![](../static/img/2024-06-15/0.png)

### 首頁

![](../static/img/2024-06-15/1.png)

### 目錄爆破

![](../static/img/2024-06-15/2.png)

### Robots.txt

![](../static/img/2024-06-15/3.png)

### secret.txt

![](../static/img/2024-06-15/4.png)

反解

![](../static/img/2024-06-15/5.png)

![](../static/img/2024-06-15/6.png)

已知有SSH key 但不知道有哪些使用者

嘗試用 wpscan 來枚舉 wordpress 的使用者

使用者為 admin

![](../static/img/2024-06-15/7.png)

![](../static/img/2024-06-15/8.png)

翻文章發現後 使用者為 oscp

嘗試用得到的 ssh key 進行登入

![](../static/img/2024-06-15/9.png)

![](../static/img/2024-06-15/10.png)

### 提權

發現有個名為 ip執行檔,但是為 root

![](../static/img/2024-06-15/11.png)

使用 grep 尋找 此程式有哪些地方在執行

![](../static/img/2024-06-15/12.png)

尋找具有root的程式

![](../static/img/2024-06-15/13.png)

![](../static/img/2024-06-15/14.png)

使用 `bash -p`

![](../static/img/2024-06-15/15.png)