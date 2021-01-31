---
title: 箭頭函式 Arrow functions
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-01-31 15:12:59
---

箭頭函式，在ES6出現的語法，有著更**簡短的語法**以及**重新定義**的 `this`。

<!--more-->
## 簡短的語法

箭頭函式與 function 的用法大致一致，可以傳入**參數**、也有**大括號**包起來，除此之外箭頭函式也有更簡短的寫法如下

```javascript=
// 正常寫法，在大括號內的 {} 是需要自行加入 return。
var callSomeone = (someone) => {
  return someone + "say Hi";
};
console.log(callSomeone("Phoebe"));

// 縮寫，單一行陳述不需要 {}
var callSomeone = (someone) => someone + "say Hi";
console.log(callSomeone("Phoebe"));

// 只有一個參數可以不加括號
var callSomeone = (someone) => someone + "say Hi";
console.log(callSomeone("Phoebe"));

// 沒有參數時，一定要有括號
var callSomeone = () => "Phoebe" + "say Hi";
console.log(callSomeone("Phoebe"));
```

## 沒有 arguments 參數

要使用 arguments 這個參數了解總共傳入了幾次並加總，但在箭頭函式內是**沒有此變數**的。

```javascript=
let Money = 1000;
const Spend = () => {
  let cash = 0;
  console.log(arguments); // arguments is not defined
}
Spend (10, 50, 100, 50, 5, 1, 1, 1, 500);
```
![](https://i.imgur.com/US9HUMX.png)


所以當需要使用 arguments 需維持使用 function

## 綁定的 this 不同

- 傳統函式：依呼叫的方法而定
- 箭頭函式：**綁定到其定義時所在的物件**

```javascript=
var name = "全域先生";
var person = {
  name: "function小姐",
  callName: function () {
    // 注意，這裡是 function，以此為基準產生一個作用域
    console.log("1", this.name); // 1 function小姐
    setTimeout(() => {
      console.log("2", this.name); // 2 function小姐
      console.log("3", this); // 3 person 這個物件
    }, 10);
  },
  callName2: () => {
    // 注意，如果使用箭頭函式，this 依然指向 window
    console.log("4", this.name); // 4 全域先生
    setTimeout(() => {
      console.log("5", this.name); // 5 全域先生
      console.log("6", this); // 6 window 物件
    }, 10);
  },
};

person.callName();
person.callName2();
```
`綁定到其定義時所在的物件`，我們要了解一般函式在建立時是在 **window** 下，所以在 window 下使用**箭頭函式**自然會指向 window。

要確實將**箭頭函式宣告在物件內部**，這樣 `this` 才會指向該物件。

簡單來說，一般函數式是建立在window下，所以箭頭函式，會指向window。但是，若將箭頭函式先告在物件內部，就會指向物件。

```javascript=
var func = function () {
  var func2 = function () {
    setTimeout(() => {
      console.log(this);
    }, 10);
  };
  // 這裡才算真正的建立一個物件
  // 因此要在此物件下的箭頭函式才會以此作為基準
  var func3 = {
    func: func2,
    var4: 4,
  };
  func2(); // this = window
  func3.func(); // func3 Object
};

func();
// 就算在這裡新增一個 function，也不會影響到內層的箭頭函式
```

![](https://i.imgur.com/tK4tg5w.png)

- `func()` 是最外層的函式，他對於內層的箭頭不會有影響。
- `func2()` 是包覆在內層的函式，但由於箭頭函式不是在物件內，所以沒有影響。
- `func3()` 是呼叫在物件內的函式，因此箭頭函式會是使用它所在的物件。

因為物件`func3`呼叫了函式`func()`，所以**箭頭函式會指向他`func3`所使用所在的物件。**

## 縮寫的方法

1. 去除function
2. 加上等號
3. 宣告變數
4. 增加箭頭
5. 去除大括號
6. 去除return 

### Arrow Function 1
```javascript=
function sum(a,b){
  return a+b;
}

// 去掉function，加上等號，宣告變數，增加箭頭
let sum2 = (a,b) =>{
  return a+b;
}

//去除return與大括號
let sum3 = (a,b) => a+b
```

### Arrow Function 2
```javascript=
function isPositive(number){
  return number >= 0;
}

let isPositive2 = number => number  >= 0
```

### Arow Function 3

```javascript=
function randomNumber(){
  return Math.random
}

let randomNumber2 = () =>  Math.random

```

### Arrow Function4

```javascript=
document.addEventListener('click',function(){
  console.log('Click');
})

document.addEventListener = ('click',function() =>  console.log('Click'))
```

## 參考文章

[JavaScript ES6 Arrow Functions Tutorial](https://www.youtube.com/watch?v=h33Srr5J9nY&list=PLZlA0Gpn_vH-0FlQnruw2rd1HuiYJHHkm&index=3)

[鐵人賽：箭頭函式 (Arrow functions)](https://wcc723.github.io/javascript/2017/12/21/javascript-es6-arrow-function/)