---
layout: post
title: "Windows 清除DNS Cache"
date: 2019-12-27 22:50:20 +0800
categories: [windows]
tags: [windows]
---

使用最高權限開啟CMD

- 指令<br>

`ipconfig /flushdns`  =>  清除 DNS 解析快取。

`ipconfig /registerdns` => 重新整理所有 DHCP 租用並重新登錄 DNS 名稱。

`ipconfig /release` => 釋放指定介面卡的 IPv4 位址。

`ipconfig /renew` => 更新指定介面卡的 IPv4 位址。

更多相關指令 請使用 `ipconfig /?` 查詢
