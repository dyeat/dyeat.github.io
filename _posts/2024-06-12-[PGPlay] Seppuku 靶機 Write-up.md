---
layout: post
title: "[PGPlay] Seppuku 靶機 Write-up"
date: 2024-06-12 01:43:02 +0800
categories: [offsec]
tags: [offsec]
---
本系列為 Proving Grounds Play Free 靶機

題目難易度為 Easy

### nmap

很多坑的一題

發現 port `21,22,80,139,445,7080,7601,8088`

![](../static/img/2024-06-12/0.png)

21 port 查找相關 Exploit 嘗試

![](../static/img/2024-06-12/1.png)

7601 Port

![](../static/img/2024-06-12/2.png)

使用 `dirb`

7601 port 發現 ckeditor

![](../static/img/2024-06-12/3.png)

8808 port 發現為Web Console

![](../static/img/2024-06-12/4.png)

卡關許多嘗試在改用其他工具重新掃描 dirsearch

80port 發現有`info.php`

![](../static/img/2024-06-12/5.png)

7601 發現名為 secret

![](../static/img/2024-06-12/6.png)

底下有個 password.lst

![](../static/img/2024-06-12/7.png)

這邊又繼續踩了坑 有個名為`r@bbit-hole`的使用者,用john 解出 依然無法登入

![](../static/img/2024-06-12/8.png)

嘗試 8088介面登入 以及 80 介面登入 最後想起有開SSH 可以直接登

![](../static/img/2024-06-12/9.png)

![](../static/img/2024-06-12/10.png)

進到系統後 會發現 cd 權限受限

僅需再輸入一次`bash` 即可

![](../static/img/2024-06-12/11.png)

## 提權

進到 /var/www底下發現都為 root 沒可利用的點

使用`sudo -l` 看權限

![](../static/img/2024-06-12/12.png)

發現無法利用

發現有個`.passwd`

![](../static/img/2024-06-12/13.png)

查看/home底下使用者資料夾 跳至其他使用者

再次使用 `sudo -l` 

![](../static/img/2024-06-12/14.png)

發現有可用/bin/ 但資料夾底下卻沒此資料夾

回到`/var/www/html` 底下查看有無目錄沒掃出來的資料夾

![](../static/img/2024-06-12/15.png)

發現有個`keys`資料夾

查看內容 看起來是ssh key

![](../static/img/2024-06-12/16.png)

使用 `ssh -i` 方式 來登入憑證

![](../static/img/2024-06-12/17.png)

進到 tanto 使用者後

經過一陣嘗試 還是無效果

回頭想起使用者`samurai` sudo -l 可讀取`.cgi_bin/bin`

建立 `.cgi_bin`

但缺了一個 bin 執行檔 , 利用echo 產生,並附於權限

![](../static/img/2024-06-12/18.png)

跳回至 `Samurai` 使用者  進行提權

![](../static/img/2024-06-12/19.png)

總結..

很多坑跳很多使用者

手法都不難,但非常考驗耐心

知識點 : 

1. 使用至少兩種不同的目錄掃描器進行探勘
2. cd受限 再次使用bash
3. 跳至不同使用者查看 sudo -l
4. ssh -i 登入憑證


