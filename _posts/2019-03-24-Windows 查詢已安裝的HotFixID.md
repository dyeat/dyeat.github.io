---
layout: post
title: "Windows 查詢已安裝的HotFixID"
date: 2019-03-24 01:15:20 +0800
categories: [windows]
tags: [windows]
---

開啟CMD

- 指令<br>
`wmic qfe`

- 訊息太長 可加 more<br>
`wmic qfe | more`

- 列出所有更新檔 只留KB開頭<br>
`wmic qfe list full | find "KB"`

- 輸出成一個html檔案<br>
`wmic qfe list full /format:htable > [路徑][檔名][格式]`
`wmic qfe list full /format:htable >.\hotfixes.htm`


