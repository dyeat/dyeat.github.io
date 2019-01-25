---
layout: post
title: "清除 Windows10 Update 暫存檔"
date: 2019-01-26 00:50:20 +0800
categories: [windows]
tags: [windows]
---

兩種方式

**一、**

設定->系統->儲存空間->立即釋放空間


**二、**

點擊開始->執行->輸入 `%systemroot%\SoftwareDistribution\Download\`

刪除Download內資料


或是將以下 存成bat檔 執行
```bat
@ECHO OFF
REM  2019-01-26 刪除 Windows Update Download暫存檔
del /S /Q %systemroot%\SoftwareDistribution\Download\

ECHO 刪除完成~
```

開啟時 必須使用系統管理員開啟<br />
`%systemroot%`底下資料若要刪除 需要系統管理員權限