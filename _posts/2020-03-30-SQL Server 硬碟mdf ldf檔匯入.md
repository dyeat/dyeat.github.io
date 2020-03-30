---
layout: post
title: "SQL Server 硬碟mdf ldf檔匯入"
date: 2020-03-30 16:20:20 +0800
categories: [sql]
tags: [sql]
---

### 一、找尋SQL Server 內 資料庫的DATA位置

此次路徑為下 大多路徑在這底下

```bat
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA
```

---

### 二、將副檔名 資料庫名稱的mdf、ldf 複製到至另一台電腦 SQL Server DATA 存放路徑

![1](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2020-03-20/1.png)

**開啟 SQL Server**

![2](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2020-03-20/2.png)

**若出現 以下畫面 無法連線**

![3](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2020-03-20/3.png)

**則可能是SQL Server 服務未開啟**

**至我的電腦(本機)-> 管理 -> 服務 找尋SQL Server(MSSQLSERVER) 的服務 -> 啟動**

![4](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2020-03-20/4.png)

![5](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2020-03-20/5.png)

---

### 三、 至SQL Server 新增資料庫

**新增查詢->輸入以下指令**
```sql

EXEC  sp_attach_db  @dbname  =  '你的資料庫名',
@filename1  =  'mdf檔案路徑(包綴名)',
@filename2  =  'Ldf檔案路徑(包綴名)'

```

![6](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2020-03-20/6.png)


![7](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2020-03-20/7.png)

**重整一次 資料表 確認資料是否匯入**

**如匯入失敗可參考以下文章 更改使用者權限**

**參考資料:[參考資料](https://www.itread01.com/p/1408783.html)**

