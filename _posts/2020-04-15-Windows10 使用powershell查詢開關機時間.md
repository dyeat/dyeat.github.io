---
layout: post
title: "Windows10 使用powershell查詢開關機時間"
date: 2020-04-15 09:55:20 +0800
img : 2020-04-15/1.png
categories: [windows]
tags: [windows]
---


**腳本結果樣式圖**

![1](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2020-04-15/1.png)


### 以下為查詢一個月內開關機紀錄腳本
```powershell

## Win10一個月內的開關機紀錄
Set-ExecutionPolicy RemoteSigned

$sHostName = hostname
$sStart_Boot = "Microsoft-Windows-Kernel-Boot"
$sShutdown = "Microsoft-Windows-Winlogon"
$Begin = (Get-Date).AddMonths(-1)
$End = Get-Date
Get-EventLog -LogName System -ComputerName $sHostName `
-After $Begin -Before $End -Source "$sStart_Boot","$sShutdown"`
 | Where-Object { $_.EventId -eq 30 -or $_.EventId -eq 7002; } `
 | SELECT-Object EventId, TimeGenerated,Source `
 | Sort-Object TimeGenerated | Format-Table -Autosize;

pause;
```

### 腳本說明

<pre>
// 找尋電腦名稱
$sHostName = hostname

// 開機來源名稱
$sStart_Boot = "Microsoft-Windows-Kernel-Boot"

// 關機來源名稱
$sShutdown = "Microsoft-Windows-Winlogon"

// 目前時間 減一個月
$Begin = (Get-Date).AddMonths(-1)

// 目前時間
$End = Get-Date

// 在本機或遠端電腦上取得事件記錄中的事件或事件記錄檔的清單。
Get-EventLog -LogName System -ComputerName $sHostName `

//  找出事件紀錄器中 30 or 7002 的事件
Where-Object { $_.EventId -eq 30 -or $_.EventId -eq 7002; }

</pre>


**參考資料:[參考資料](https://forsenergy.com/zh-tw/windowspowershellhelp/html/a4372a60-b7d9-4b1c-a268-aa5240300141.htm)**
