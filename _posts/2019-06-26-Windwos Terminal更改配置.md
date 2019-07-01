---
layout: post
title: "Windwos Terminal 配置"
date: 2019-06-25 15:25:20 +0800
categories: [windows]
tags: [windows]
---

---

### 完成圖
![](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2019-06-26/2.png)

---

### Windows Terminal下載

Windows 10 版本 1903後 可至 [Microsoft store](https://www.microsoft.com/zh-tw/p/windows-terminal-preview/9n0dx20hk701?activetab=pivot:overviewtab) 下載 `Windows Terminal`


---

### Windows 版本查詢

開啟CMD

- 指令 `winver`

![](https://raw.githubusercontent.com/dyeat/dyeat.github.io/master/static/img/2019-06-26/1.png)



---

更改配置 開啟 `Windows Terminal` -> `CTRL + ,`


找尋 `defaultProfile` 更改預設開啟使用的`Terminal` 預設為`Powershell`
```json
    "globals" :
    {
        "alwaysShowTabs" : false,
        "defaultProfile" : "{6e5se0344-xxxx-xxxx-xxxx-7015s457w01x}",
        "initialCols" : 120,
        "initialRows" : 30,
        "keybindings" :
```

---

### 更改Terminal背景

將圖片下載至
<pre>%LOCALAPPDATA%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState</pre>

對應終端機插入 以下三行 更改背景圖檔名
![](https://devblogs.microsoft.com/commandline/wp-content/uploads/sites/33/2019/06/background-image-code-snip.png)


**更多修改資訊 參考[官方文件](https://devblogs.microsoft.com/commandline/windows-terminal-microsoft-store-preview-release/)**

