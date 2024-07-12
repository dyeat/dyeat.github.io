---
layout: post
title: "[PGPractice] Algernon  靶機 Write-up"
date: 2024-07-12 14:23:02 +0800
categories: [offsec]
tags: [offsec]
---

本系列為 Proving Grounds Play Subscription 靶機

## 官方難易度 : Easy

## 社群評論難易度 :

## 解題花費時間 : < 120 min

## 知識點 :

## Port Scan

![](../static/img/2024-07-12/0.png)

## 80 Port

![](../static/img/2024-07-12/1.png)

## 445 Port

smbclient Access_denied

enum4linux 沒東西

![](../static/img/2024-07-12/2.png)

## 135 Port Connect ACCESS_DENIED

![](../static/img/2024-07-12/3.png)

## 17001 Port

![](../static/img/2024-07-12/4.png)

## 21  FTP 可匿名登入

帳號與密碼 anonymous

![](../static/img/2024-07-12/5.png)

在logs裡面 發現 `2020.05.12-administrative.log`   

![](../static/img/2024-07-12/6.png)

## 9998 Port

![](../static/img/2024-07-12/7.png)

尋找 SmarterMail Exploit

使用 CVE-2019-7214 進去系統

![](../static/img/2024-07-12/8.png)

發現outpu.txt

![](../static/img/2024-07-12/9.png)

最高權限的桌面發現 proof.txt

![](../static/img/2024-07-12/10.png)