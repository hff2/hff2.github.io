---
title: '[JS30] Day2 - JS + CSS Clock'
author: Phoebe
tags: Javascript
categories: JS 30
date: 2021-05-1 11:07:11
---

## 學習到的知識點

- 透過 CSS 選擇元素 (`querySelector`)
- Date 時間物件
- 取得日期物件的本地時間 (`getHours`，`getSeconds`，`getMinutes`)
- 透過 JS 控制 CSS (`style.transform`)
- JS 計時器 (`setInterval`，`setTimeout`，`requestAnimationFrame`)
<!--more-->

## 思考分析

1. 取得本地時間，顯示在時鐘上。
2. 計算每秒要改變的角度
3. 角度更新到時鐘，改變時鐘每秒狀態。

### 1. 取得時針，分針，秒針

在開始撰寫程式之前，先使用立即函式(IIFE)將整個程式包起來，進行封裝。

在前面打個分號的用意為，當載入比較多東西時，有個分號會比較保險。

```javascript=
;(function(){

})()
```

`querySelector`：JS 原生 CSS 選擇器，需要注意的地方是，若找不到相對應的元素會回傳 null，否則會回傳第一個符合的元素。所以，如果是多個屬性具有相同的名稱時，他只會選擇到第一個符合的元素。

選取時針 (`hour`)，分針 (`min`)，秒針 (`second`)。

```javascript=
const second = document.querySelector('.second-hand')
const min = document.querySelector('.min-hand')
const hour = document.querySelector('.hour-hand')
```

### 2. 建立函式，計算每秒要改變的角度

使用 `new Date` 建立一個 Date 物件。

再使用 `getSeconds()` - 取得幾秒，`getMinutes` - 取得幾分， `getHours` - 取得幾小時。

- 秒數後面的乘 6，是因為 ( 360 度 / 一圈 60 秒 )。所以，一秒代表六度。
- 分鐘與秒是相同的道理。
- 小時後面的乘 30，是因為 ( 360 度 / 一圈 12 小時 )。所以，一小時代表 30 度。

`hourDeg` 後面加上 `data.getSeconds() * 6/60`，意思為一小時有 60 分鐘，每分鐘移動 6 (360/60) 度。讓時間再跑的同時，時針也可以有細微的變動，屬於比較細節的部份。

`minDeg`，是相同的意思。

```javascript=
function setClock(){
  // 獲得時間物件
  let data = new Date();

  let secondDeg = data.getSeconds() * 6; //(360/60sec)
  let minDeg = data.getMinutes() * 6+ data.getSeconds() * 6/60; //(360/60min)
  let hourDeg = data.getHours() * 30 + data.getMinutes() * 30/60; //(360/12hr)
```

### 3. 將計算好的角度，更新到時鐘上

透過 JS 控制 CSS，使用 `.style.transform = rotate` ，就可以將角度更新到時鐘上。

```javascript=
function setClock(){
  second.style.transform = `rotate(${secondDeg}deg)`;
  min.style.transform = `rotate(${minDeg}deg)`;
  hour.style.transform = `rotate(${hourDeg}deg)`;
}
```

### 4. 每秒更新時鐘的狀態

這邊會講解三種計時器的運用。

- `setInterval`
- `setTimeout`
- `requestAnimatoin`

#### 第一種用法 `setInterval`

固定延遲了某段時間之後 ( 在這邊是 1000 毫秒 )，才去執行對應的程式碼，然後「不斷循環」。

**設定間隔，持續執行。**

```javascript=
setInterval(setClock,1000);
```

#### 第二種用法 `setTimeout`

此用法像是球賽喊暫停一樣，所以需要呼叫自己達到連續的動作。

**設定延遲，執行一次。**

```javascript=
function timeoutHandler(){
  setClock();
  setTimeout(timeoutHandler,1000); // 呼叫自己
}

setTimeout(timeoutHandler,1000);
```

#### 第三種用法 `requestAnimatoin`

和`setTimeout`十分相似，他也需要呼叫自己，但`requestAnimatoin`屬於專門處理畫面的用法。

```javascript=
function animationHandler(){
  setClock();
  window.requestAnimationFrame(animationHandler);
}

window.requestAnimationFrame(animationHandler);
```

## 延伸學習

[Javascript 中的 setTimeout 與 setInterval](https://hackmd.io/@PhoebeHo/rkizdu9w_)

## 參考網站

[transform - CSS | MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/transform)

[JavaScript Date 時間和日期 - JavaScript (JS) 教學 Tutorial](https://www.fooish.com/javascript/date/)

[JavaScript Timer setTimeout(), setInterval() 計時器 - JavaScript (JS) 教學 Tutorial](https://www.fooish.com/javascript/timer.html)

[談談 JavaScript 的 setTimeout 與 setInterval | Kuro's Blog](https://kuro.tw/posts/2019/02/23/%E8%AB%87%E8%AB%87-JavaScript-%E7%9A%84-setTimeout-%E8%88%87-setInterval/)
