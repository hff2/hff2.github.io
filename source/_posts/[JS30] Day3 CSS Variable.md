---
title: '[JS30] Day3 - CSS Variable'
author: Phoebe
tags: Javascript
categories: JS 30
date: 2021-05-3 11:07:11
---

## 學習到的知識點

## 思考分析

1. 選取所有的`input`
2. 判斷更改哪一個`input`(padding，blur，color)
3. 更改`input`後，可以觸發網頁上的元件產生變化

<!--more-->

![](https://i.imgur.com/JJtF4ua.png)

### 1. 選取所有的`input`

`querySelectorAll`選出來的不是純陣列。

有人稱他像是半殘的 Array。

(待補充)

```javascript=
const inputs = document.querySelectorAll(".controls input");
```

### 2. 監聽事件

`change`這個事件是做在最後，所以當滑鼠在來回移動時，他並不會被觸發。

所以加上`changeHandler`就可以偵測來回移動時的變數。

```javascript=
inputs.forEach(function(input){
    input.addEventListener('change',changeHandler)
    input.addEventListener('mousemove',changeHandler)
})
```

### 3. 撰寫函式

這裡的`dataset`是寫在 HTML 裡。

![](https://i.imgur.com/UWzebSh.png)

藉由`dataset`來判斷他是否有單位。如果有單位的話，就加上，沒有單位的話，就為空值。

```javascript=
function changeHandler(){
  const unit = this.dataset.sizing || '';
  document.documentElement.style.setProperty(`--${this.name}`, this.value + unit);
}
```

## 延伸學習

## 參考網站
