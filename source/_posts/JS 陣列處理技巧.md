---
title: 'JS 陣列處理技巧'
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-05-31 11:07:11
---

在練習 JS30 Day4 的這段時間，剛好看到六角學院卡斯柏的 [JS 陣列處理技巧直播](https://www.youtube.com/watch?v=_vFuDQ_6Xt8)，這篇會將影片內容記錄下來，也加深自己的印象。

在開始之前，先提及一張圖搞懂 JS array 函式，這張圖是一位[波蘭工程師](https://twitter.com/sulco/status/1281545450273865730)分享在 Twitter 上的，非常厲害。

<!--more-->

![](https://i.imgur.com/hSHZMZS.jpg)

## 前言

每一個題目會分成原始 `forEach` 的做法，與使用 `prototype` 的用法。

總共七個題目：

情境：卡斯伯一行人決定到麵店內用，點了以上餐點以後...

1. 請一一列出每個人的訂單
2. 小明看到今天有打八折！！，請將所有訂單新增一個新價格，金額是 80%
3. 老闆說，今天疫情沒有八折啦，不過 80 元的可以給滷蛋
4. 過一段時間後，老闆發現牛肉沒了，把點牛肉麵的換成牛肉湯麵
5. 老闆說 POS 機壞了，麻煩幫忙出一下 LI 結構，方便列印發票
6. 老闆要收錢了，請問老闆應該收多少錢
7. 今天誰吃最貴！請排序所有的金額

## 資料內容

```javascript=
const people = [
        {
            name: '卡斯伯',
            order: '鍋燒意麵',
            price: 80
        },
        {
            name: '小明',
            order: '牛肉麵',
            price: 120
        },
        {
            name: '漂亮阿姨',
            order: '滷味切盤',
            price: 40
        },
        {
            name: 'Ray',
            order: '大麻醬乾麵',
            price: 60
        },
    ];
```

## 1. 請一一列出每個人的訂單

![](https://i.imgur.com/LhwI9UV.png)

### 第一種方法 - `forEach`

```javascript=
let mapItem = people.forEach(function(item,key){
    console.log(item);
});
```

### 第二種方法 - `map`

```javascript=
let mapItem = people.map(function(item,key){
    return item;
});
console.table(mapItem);
```

### 第三種方法 - `map` + `arrowFucntion`

```javascript=
let mapItem = people.map((item,key)=>item);
console.table(mapItem);
```

## 2. 請將所有訂單新增一個新價格，金額是 80%

![](https://i.imgur.com/GINtzC3.png)

### 第一種方法 - `forEach`

這邊使用到 `...`，是一種展開式。可以更方便讀取每一個值，加上 `[key]`的使用，可以讓每一個值都乘上 0.8 ，屬於 ES6 的語法。

```javascript=
const newOrders = [];
people.forEach(function(obj,key){
    // 第一種寫法
    // newOrders.push(obj);

    // 第二種寫法
     newOrders[key] = {
         ...obj,
         newPrice: obj.price * 0.8,
     }
 });
```

### 第二種方法 - `map`

`map` 會自己產生新的陣列，因此不需要跟 `forEach`一樣，自己先宣告一個空陣列。

```javascript=
let newOrders = people.map(function(obj,key){
    return{
        ...obj,
        newPrice: obj.price * 0.8,
    }
});
console.table(newOrders);
```

### 第三種方法 - `map` + `arrowFucntion`

變成箭頭函式的準則：

- 去掉 `return`
- 大括號
- 去掉 `function`

```javascript=
const newOrders = people.map((item,index)=>
    ({
        ...item,
        newPrice: item.price*0.8,
    })
);
```

## 3. 老闆說，今天疫情沒有八折啦，不過 80 元的可以給滷蛋

![](https://i.imgur.com/R26qlH4.png)

### 第一種方法 - `forEach`

```javascript=
const newOrders2 = [];
people.forEach(function(item,index){
    if(item.price >= 80){
        newOrders2.push(item);
    }
});

console.table(newOrders2);
```

### 第二種方法 - `filter`

```javascript=
const newOrders = people.filter(function(item,index){
    return item.price >= 80;
})
console.log(newOrders)
```

### 第三種方法 - `filter` + `arrowFucntion`

```javascript=
const newOrders = people.filter((item,index)=> item.price >= 80)
console.table(newOrders)
```

## 4. 過一段時間後，老闆發現牛肉沒了，把點牛肉麵的換成牛肉湯麵

### 第一種方法 - `forEach`

```javascript=
let index = 0;
people.forEach(function(obj,key){
    if(obj.order === "牛肉麵"){
        index = key;
    }
});
people[index].order = "牛肉湯麵";

console.log(people[index]);
```

### 第二種方法 - `map`

```javascript=
const index = people.findIndex(function(item){
    return item.order === "牛肉麵";
});
people[index].order = "牛肉湯麵";
```

### 第三種方法 - `map` + `arrowFucntion`

```javascript=
const index = people.findIndex((item)=>item.order === "牛肉麵");
people[index].order = "牛肉湯麵";
console.table(people[index]);
```

## 5. 老闆說 POS 機壞了，麻煩幫忙出一下 LI 結構，方便列印發票

### 第一種方法 - `forEach`

```javascript=
let htmlTemplate = " ";
people.forEach(function(obj,key){
    htmlTemplate = htmlTemplate + `<li>
        ${obj.order},${obj.price}
    </li>`;
});
console.log(htmlTemplate);
```

### 第二種方法 - `map`

```javascript=
const htmlTemplate = people.map(function(obj,key){
    return `<li>
        ${obj.order},${obj.price}
    </li>`;
}).join('');

// map會回傳陣列的結果
console.log(htmlTemplate);
```

### 第三種方法 - `map` + `arrowFucntion`

```javascript=
const htmlTemplate = people.map((obj,key)=>
    (`<li>${obj.order},${obj.price}</li>`)).join('');

console.log(htmlTemplate)
```

## 6. 老闆要收錢了，請問老闆應該收多少錢

### 第一種方法 - `forEach`

```javascript=
let total = 0;
people.forEach(function(obj,key){
    total += obj.price;
});
console.log(total);
```

### 第二種方法 - `reduce`

```javascript=
let total = people.reduce(function(acc,cur){
    return acc += cur.price;
},0);
console.log(total);
```

### 第三種方法 - `map + arrowFucntion`

```javascript=
let total = people.reduce((acc,cur)=>(acc += cur.price),0);
console.log(total);
```

## 7. 今天誰吃最貴！請排序所有的金額

### 第一種方法 - `sort`

```javascript=
let sortItem = people.sort((a,b)=>a.price - b.price)
console.table(sortItem);
```

## 後記

在練習完 JS30 的 Day4 後，還是對 Array 的操作不是很熟悉。很剛好的在遇到一知半解的時候，有許多資源可以讓自己學的更透徹。期望自己的筆記也能幫助到別人，也希望 JS30 的學習可以繼續努力下去，將 30 篇筆記寫完。
