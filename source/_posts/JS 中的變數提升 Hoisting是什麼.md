---
title: "JS 中的變數提升 Hoisting是什麼"
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-04-13 11:07:11
---

## 什麼是 Hoisting?

Hoisting 就是「提升」的意思。

<!--more-->

```javascript=
console.log(i)
//Uncaught ReferenceError: i is not defined
```

舉例來說，當只有`console.log`時，就會出現 not defined，因為我們試圖去對一個**還沒被宣告的變數**取值，才會出現此錯誤。

```javascript=
console.log(i)
var i
//undefined
```

上面的例子中，是在下方 ( 第二行 ) 宣告變數時，會出現 undefined，此現象就叫做**Hoisting**。

不同於以往我們對程式的認知為一行一行跑，第二行的`var i`，因為某些原因，被提升到了最上面。

```javascript=
console.log(i)
var i = 5
//undefined
```

但是變數提升，只會提升變數的宣告會提升。**賦與的值( 賦值 )並不會被提升**。依然會是 undefined。

```javascript=
// PART 1
function test(i){
    console.log(i);
    var i;
}
test(10)
// 10

// PART2
function test(i){
    var i = 10;
    console.log(i);
    var i;
}
test(10)
```

當以 function 宣告的時候，會出現`10`，而不是 `undefined`。

因為值會是以 PART2 的樣子，出現在 Function 的第一行，就被宣告且賦值了！

最後，functoin 的宣告也會提升而且優**先權較高**，所以程式會輸出`function`而不是`undefined`。

```javascript=
console.log(a)
var a
function a(){}
// [Functoin: a]
```

## `let` `const` `var` 與 hoisting

### `let` `const`

`let` `const` `var` 最主要的差異是：ES6 `let` 和 `const` 以「區塊」作為其作用域 ( scope )。而 `var` 以「函數」作為其作用域。

`let` 與 `const` 換句話說，就是只有在**區域**裡面才看的到。以下方的例子來說。

```javascript=
{
  let name = "Phoebe";
  console.log(name); // Phoebe
}
console.log(name); // undefined
```

`name` 這個變數只有在大括號裡，也就是區域內才看的到。

### `var`

`var` 的作用域是函式作用域 ( function-level scope )。

換句話說就是，用 `var` 宣告的變數，只有在「函式」裡可以看得到。

## 為什麼我們需要 hoisting 呢？

可以從反向思考，「如果沒有 hoisting 會怎麼樣?」

1. 一定要宣告變數才可以使用 (其他語言的習慣)
2. 一定要宣告函式才可以用 (特別注意)
3. 沒有辦法達成 function 互相呼叫

舉個例子

```javascript=
function loop(n){
    if (n>1) {
        show(--n)
    }
}

function show(n) {
    console.log(n, n % 2 ? '奇數' : '偶數')
    loop(n)
}
loop(20)
```

我們在 loop 裡面呼叫 `show()`，在 `show()` 裡面也呼叫 `loop()`，如果沒有 hoisting ，以上程式碼就不會達成。

因為，不可能做到 A 在 B 上面，而 B 又在 A 上面。

所以 hoisting 就是為了解決上述的問題 !

## 參考文章

[我知道你懂 hoisting，可是你了解到多深？](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/)

[[教學] JavaScript 中的 Hoisting 是什麼意思？let const var 的差異居然是這個？ | Shubo 的程式教學筆記](https://shubo.io/javascript-hoisting/)
