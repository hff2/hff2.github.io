---
title: Hoisting 變數提升是什麼
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-04-13 15:12:59
---

## 什麼是 Hoisting?

Hoisting 就是「提升」的意思。

舉例來說，當只有`console.log`時，就會出現 not defined，因為我們試圖去對一個**還沒被宣告的變數**取值，才會出現此錯誤。

<!--more-->

```javascript=
console.log(i)
//Uncaught ReferenceError: i is not defined
```

但是在下方宣告變數時，會出現 undefined，此現象就叫做**Hoisting**。

不同於以往我們對程式的認知為一行一行跑，第二行的`var i`，因為某些原因，被提升到了最上面。

```javascript=
console.log(i)
var i
//undefined
```

但是變數提升，只會提升變數的宣告會提升。賦與的值(賦值)並不會被提升。依然會是 undefined。

```javascript=
console.log(i)
var i = 5
//undefined
```

當以 function 宣告的時候，會出現`10`，而不是`undefined`。

因為值會是以 PART2 的樣子，出現在 Function 的第一行，就被宣告且賦值了！

```javascript=
// PART 1
function test(i){
    console.log(i);
    var i;
}
test(10)

// PART2
function test(i){
    var i = 10;
    console.log(i);
    var i;
}
test(10)
```

最後，functoin 的宣告也會提升而且優先權較高，所以程式會輸出`function`而不是`undefined`。

```javascript=
console.log(a)
var a
function a(){}
// [Functoin: a]
```

## let 跟 const 與 hoisting

## 為什麼我們需要 hoisting？

## hoisting 到底是怎麼運作的？

## 參考文章

[我知道你懂 hoisting，可是你了解到多深？](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/)

[[教學] JavaScript 中的 Hoisting 是什麼意思？let const var 的差異居然是這個？ | Shubo 的程式教學筆記](https://shubo.io/javascript-hoisting/)
