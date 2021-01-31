---
title: 什麼是 Callback Function?
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-01-25 19:37:11
---
## 簡介

Callback Function，又稱回呼函式，簡單來說，就是在**一支函式執行完後，才要執行的函式。**

在 ES6 中的 Promise 語法還未能使用前，就很常使用 Callback function 來接收**非同步的資料**。
<!--more-->
例如一支函式`First()`，在執行結束才執行`Second()`，這個`Second()`就是一支Callback Function。

### 舉例來說

> 程式碼
 
```javascript=
var First = function (callback) {
console.log("First");
callback();
};
var Second = function () {
console.log("Second");
};
First(Second); //呼叫Second()
```

> 輸出：

![](https://i.imgur.com/xuvoDQ7.png)

跟下面這段程式是相同的。

> 程式碼

```javascript=
var First = function () {
 console.log("First");
};
var Second = function () {
 console.log("Second");
};
```

> 輸出：

![](https://i.imgur.com/xuvoDQ7.png)

但是，如果是以下的情況就不同了。

## 非同步處理 Asynchronous 

原本`First()`中直接印出First文字的工作，改交給`setTimeout()`這個非同步(Asynchronous)程式處理。

`setTimeout()`的第一個參數為**時間到時要被執行的程式**，第二個參數為**要延遲的時間（毫秒）**。

```javascript=
var First = function () {
setTimeout(function () {
  console.log("First");
}, 3000); // 非同步，3秒後才執行
};
var Second = function () {
console.log("Second");
};
First();
Second();
```

> 輸出：

![](https://i.imgur.com/8e9qDvH.png)

為什麼Second會出現在First上面?

因為`setTimeout()`是非同步，所以下面的`Second()`**不須等待**`First()`執行完就會先被執行了。

所以為了確保`Second()`，要在`First()`中的`setTimeout()`**後**執行。

我們可以將`Second()`做為**callback函式以參數**傳入`First()`。

```javascript=
var First = function (callback) {
setTimeout(function () {
  console.log("First");
  callback(); //在印出First之後，才印出Second
}, 3000); 
};
var Second = function () {
console.log("Second");
};
First(Second);
```
### 同步與非同步的差異?

![](https://i.imgur.com/qrIV88s.png)

同步(Synchronous)，指程式**必須**等待前面的程式執行完才能執行。

非同步(Asynchronous)，指程式**不須**等待前面的程式執行完就能執行。

同步就像只有一個隊伍，而非同步有好幾個隊伍執行。

## 結論

因此Callback function的作用，是保證一支程式會在一支程式執行後才執行。

至於被傳入callback函式的函式，也就是上面的`First(callback)`，又稱為Higher Order Function（高階函式）。

所以Callback Function又可以解釋為「以參數型態傳入另一個函式的函式」。

白話一點就是，把函式當作另一個函式的參數，透過另一個函式來呼叫它。

### 補充

當函式之間的相依過深，callback太多層之後，就會出現很常看到，解說文章裡的波動拳圖片XD。

![](https://i.imgur.com/T2dnFh7.jpg)

如果真的必須要寫到多層，就可以使用Promise來避免這種情況。

## 參考文章

[JavaScript 什麼是Callback函式 (Callback Function)？](https://matthung0807.blogspot.com/2019/05/javascript-callback-callback-function.html)

[JavaScript 一級函式 （First Class Functions）](https://wcc723.github.io/development/2020/09/24/first-class-function/)

[重新認識 JavaScript: Day 18 Callback Function 與 IIFE](https://ithelp.ithome.com.tw/articles/10192739)