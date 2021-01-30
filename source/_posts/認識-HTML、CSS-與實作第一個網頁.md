---
title: 認識 HTML、CSS 與實作第一個網頁
author: Phoebe
date: 2020-11-31 02:20:52
tags: HTML
categories: Web
---
## HTML是什麼?

![](https://i.imgur.com/ICRsLf0.png)

HTML(HyperText Markup Language)是一種超文本標記語言，不算是程式語言。

主要功能為告訴瀏覽器有哪些「元素」，而元素(Element)的組成為標籤(tags)+內容(content)。

<!--more-->

標籤分為起始標籤和結束標籤，中間放內容。元素還會有屬性（Attribute）



HTML是由「巢狀元素（nest element）」構成的。

每個元素都有自己的起始以及結束標籤，並一層層包覆。

```htmlembedded=
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  
</body>
</html>
```

在HTML5這個版本，強化了文件結構。

能分類內容、選單...等元素，電腦就能正確解釋並呈現HTML中的內容。

搜尋引擎就能快速找到網頁的標籤，進而提升搜尋引擎的精確度。結構強化對SEO優化有很大的幫助。

---
## 解析HTML
```htmlembedded=
<!DOCTYPE html>
```
* 一份標準的HTML文件中，在第一行都會有`<!DOCTYPE html>`。

* DOCTYPE是Document Type的簡寫，也就是文件類型的意思。

* 告訴瀏覽器這是一份以「HTML標記語言(markup language)」所撰寫的文件，所以請用HTML的定義來解讀我。

---
```htmlembedded=
<html lang="en"></html>
```
* `<html></html>`為用來包住整個html的程式碼，在開頭會加入`lang="en"`為語言判定標籤。

* 告訴搜尋引擎判斷網頁的內容為何，並不會影響網頁呈現。

* 若寫 `<html lang="en">`，就代表沒有特定的地區！

---
```htmlembedded=
<head></head>
```
* HTML的head元素會包含title，style，meta，link和script。

* `meta charset="utf-8"`指定網頁內容是用什麼編碼(character set)，現在大多數的網頁編碼都是UTF-8。
---
```htmlembedded=
<title></title>
```
* 分頁欄看見的文字，預設為Document。

---
```htmlembedded=
<body></body>
```
* 網頁的內容。

---

## CSS
階層式樣式表(Cascading Style Sheets)

可以在index.html裡使用`<style> </style>`標籤，也能夠另外開檔案(style.css)再使用link引入。

![](https://i.imgur.com/RxEKEfV.png)

## Javascript

可以在index.html裡使用`<script></script>`標籤，也能夠另外開檔案(app.js)再使用link引入。

不過需要放在`</body>`前面才會有作用，因為，瀏覽器分析HTML檔案，是由上而下分析。需要等DOM解析完後，才可以抓取到JS控制的元素。

---

## 試著用cmd建立自己的第一個網頁
1. 先新增資料夾

![](https://i.imgur.com/2MVM4Gu.png)

2. 新增檔案

![](https://i.imgur.com/Kx6jHmA.png)

3. code . 打開vscode

Emment語法我是以 驚嘆號(!)+tab展開。

![](https://i.imgur.com/EKyxga1.png)

4. 打完之後，將滑鼠放到檔案上，按下右鍵 open with live server就可以打開瀏覽器。

![](https://i.imgur.com/FMyZgbw.png)
