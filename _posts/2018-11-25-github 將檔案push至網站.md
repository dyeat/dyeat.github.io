---
layout: post                          
title: "github 將檔案push至網站"                   
date: 2018-11-25 22:51:02 +0800       
categories: [others, bash]         
tags: [github]                     
---

- **初始化**
1. <pre>git init</pre> 
- **新增一個說明檔 或指定資料夾** 
2. <pre>git add README.md</pre>  
- **commit 編輯說明**
3. <pre>git commit -m "first commit"</pre> 
- **查看當前狀態 ※步驟可省略**
4. <pre>git status</pre>
- **指定 要上傳到哪個專案** 
5. <pre>git remote add origin https://github.com/dyeat/dyeat.github.io.git</pre>
- **將檔案推上去 推至哪個來源**
6. <pre>git push -u origin master</pre>

