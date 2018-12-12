---
layout: post                          
title: "Linux 忘記密碼 以 GRUB 開機進入單機模式 修改 root 密碼"
date: 2018-12-12 18:57:00 +0800       
categories: [linux]         
tags: [linux]                     
---




Linux 忘記密碼 以 GRUB 開機進入單機模式(Single User Mode) 修改 root 密碼
忘記 Linux 密碼導致無法登入是一個很常見的問題，如果是初學者不會處理，最後無可奈何大都只好重灌，其實重設 Linux 密碼的過程並不難，以下我們以 Ubuntu Linux 為例，示範如何以 GRUB 開機進入單機模式（Single User Mode），用指令重新設定 Linux 的密碼。

### STEP 1
在開機時，按下鍵盤左邊的`「Shift」`鍵或是左上角的`「Esc」`鍵，開啟 GRUB 開機選單。
![https://dyeat.github.io/static/img/2018-12-12/grub.png](https://dyeat.github.io/static/img/2018-12-12/grub.png)

看到這個畫面時，您可以使用上下鍵選擇開機的模式或是記憶體測試，這裡我們選擇第一個正常開機的選項，然後按下鍵盤上的「e」鍵。

### STEP 2
接著會看一個參數編輯的視窗。

![https://dyeat.github.io/static/img/2018-12-12/grub-2.png](https://dyeat.github.io/static/img/2018-12-12/grub-2.png)

### STEP 3
尋找有 <pre>linux /boot/vmlinuz-X.XX.X</pre> 字樣開頭的那一行。

![https://dyeat.github.io/static/img/2018-12-12/grub-3.png](https://dyeat.github.io/static/img/2018-12-12/grub-3.png)

### STEP 4
在 <pre>linux /boot/vmlinuz-X.XX.X</pre> 這一行的最後，加上 single 參數。

![https://dyeat.github.io/static/img/2018-12-12/grub-4.png](https://dyeat.github.io/static/img/2018-12-12/grub-4.png)

<pre>linux /boot/vmlinuz-X.XX.X</pre> 這一行在不同的 Linux 版本可能有些差異，不過這裡並不會有影響，不管中間的內容是什麼，只要在結尾加上 single 參數即可。
### STEP 5
編輯好參數之後，按下 `Ctrl + x` 或是 `F10` 開機，接著就會進入單機模式。單機模式的畫面會類似這樣：

![https://dyeat.github.io/static/img/2018-12-12/grub-5.png](https://dyeat.github.io/static/img/2018-12-12/grub-5.png)

### STEP 6
在單機模式之下，使用 `passwd` 更改一般使用者（或 `root`）的密碼：

![https://dyeat.github.io/static/img/2018-12-12/grub-6.png](https://dyeat.github.io/static/img/2018-12-12/grub-6.png)

這裡示範是更改一般使用者的密碼，如果要直接更改 `root` 的密碼，就直接執行 passwd 不要加任何參數即可。

### STEP 7
最後執行 `reboot` 重新開機，就可以用新的密碼登入了。

資料來源<br />
[https://blog.gtwang.org/linux/linux-grub-change-root-password/](https://blog.gtwang.org/linux/linux-grub-change-root-password/)