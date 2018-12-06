---
layout: post
title: "[WSL]Windows Subsystem for Linux"
date: 2018-12-06 16:55:20 +0800
categories: [others]
tags: [windows]
---

### 使用MicrosoftStore 安裝 Ubuntu 子系統

Windows10 組建大於 14393時 可安裝 Ubuntu 子系統

### 查看組建版本 
<pre>開始 -> 設定 -> 系統 -> 關於</pre>

![](https://dyeat.github.io/static/img/2018-12-06/Windows-version.PNG)


### 至 Michosoft Store 尋找 ubuntu -> 安裝
![](https://dyeat.github.io/static/img/2018-12-06/Ubuntu.PNG)

 ### 出現
 `error:0x8007019e`

<pre>Installing, this may take a few minutes...
WslRegisterDistribution failed with error: 0x8007019e
The Windows Subsystem for Linux optional component is not enabled. Please enable it and try again.
See https://aka.ms/wslinstall for details.
Press any key to continue...</pre>

原因：未安裝 Windows子系統支持<br />
1.Win + x，選擇Windows PowerShell（管理員）<br />
2.輸入：<pre>Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux<pre><br />
3.Enter，輸入Y，重新啟動！<br />

![](https://dyeat.github.io/static/img/2018-12-06/WSL.PNG)
4.重新打開已經安裝的子系統，等幾分鐘，輸入帳號和密碼，完成。




