---
title: '[JS30] Day3 - CSS Variable'
author: Phoebe
tags: Javascript
categories: JS 30
date: 2021-05-3 11:07:11
---

## 學習到的知識點

- `querySelector` 與純陣列的差異
- `dataset` 的使用方法
- `document.documentElement` 為網頁的根元素
- 事件監聽 `change` 與 `mousemove`
- CSS 變數，( 宣告：`--名稱：值` )
<!--more-->

## 思考分析

1. 選取所有的 `input` (可以被調整的地方)
2. 判斷更改哪一個 `input` (`padding`，`blur`，`color`)
3. 更改 `input` 後，可以觸發網頁上的元件產生變化。

### 1. 選取所有的`input`

`querySelectorAll` 選出來的不是純陣列。

有人稱他像是半殘的 Array。

(待補充)

```javascript=
const inputs = document.querySelectorAll(".controls input");
```

### 2. 監聽事件

`change` 這個事件是做在最後，所以當滑鼠在來回移動時，他並不會被觸發。所以再加上 `mousemove` 就可以偵測到所有的移動。

加上`changeHandler`函式，就可以偵測來回移動時的變數。

```javascript=
inputs.forEach(function(input){
    input.addEventListener('change',changeHandler)
    input.addEventListener('mousemove',changeHandler)
})
```

### 3. 撰寫函式

以下三種寫法為同一種，都可以取到網頁的根元素。

![](https://i.imgur.com/ilhxfhi.png)

```javascript=
document.querySelector(":root")
document.querySelector("html")
document.documentElement
```

這裡的`dataset`是寫在 HTML 裡。

![](https://i.imgur.com/UWzebSh.png)

藉由`dataset`來判斷他是否有單位。如果有單位的話，就加上，沒有單位的話，就為空值。

[data-\* attribute 是什麼 ?](https://hff2.github.io/2021/04/22/HTML5%20%E4%B8%AD%E7%9A%84%E8%B3%87%E6%96%99%E5%B1%AC%E6%80%A7/)

因為作者 Wes Bos 使用了`data-sizing`這個自定義的資料屬性，所以要取得 `data-* attribute` 的屬性值時，我們可以使用 JavaScript 中的 `dataset` 物件。

`setProperty`，自己的理解為，可以利用 JS 即時的更改 CSS 的樣式。例如：按鈕被觸發時，當滾輪移動時。

```javascript=
function changeHandler(){
  const unit = this.dataset.sizing || '';
  document.documentElement.style.setProperty(`--${this.name}`, this.value + unit);
}
```

## 延伸學習

[HTML 5 中的資料屬性（data-\* attribute） | Phoebe's Blog](https://hff2.github.io/2021/04/22/HTML5%20%E4%B8%AD%E7%9A%84%E8%B3%87%E6%96%99%E5%B1%AC%E6%80%A7/)

[深入理解 CSS 變數 ( CSS Variables ) - OXXO.STUDIO](https://www.oxxostudio.tw/articles/202011/css-variables.html)

## 參考網站

[CSSStyleDeclaration.setProperty() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration/setProperty)
