---
layout: post                          
title: "github 將檔案push至網站"                   
date: 2018-11-25 22:51:02 +0800       
categories: [others, bash]         
tags: [github]                     
---

### github 將檔案push至網站

1. `git init`  // 戳一個.git出來
2. `git add README.md`  // 新增一個說明檔 或指定資料夾 
3. `git commit -m "first commit"` // commit 一個紀錄
4. `git status` // 查看當前狀態 ※步驟可省略 
5. ` git remote add origin https://github.com/dyeat/dyeat.github.io.git` //指定 要上傳到哪個專案 
6. `git push -u origin master`  // 將檔案推上去 推至哪個來源 

