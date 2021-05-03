---
title: '[JS30] Day 1 JS Drum Kit'
author: Phoebe
tags: Javascript
categories: JS 30
date: 2021-04-24 11:07:11
---

## 學習到的知識點

- 事件監聽 (`addEventListener(event,function)`)
- 按鍵事件 (`keydown`，`keyup`，`keypress`)
- 透過 CSS 選擇元素 (`querySelector`，`querySelectorAll`)
- 音效控制（`element.play( )`，`element.currentTime`)
<!--more-->
- 資料屬性（`data-* attribute`)
- CSS 相關（`element.classList.add( )`，`element.classList.remove( )`)
- 動畫結束事件 `transitionEnd`
- `forEach( )`
- 若不符合則退出函式：`function( ){if(...) return}`

## 思考分析

1. 瀏覽器可以判斷使用者在鍵盤按下的鍵
2. 按下指定的按鍵後，可以回傳指定的音效
3. 按下指定的按鍵後，可以觸發網頁上的元件產生變化
4. 網頁上的元件要能夠恢復成原本的樣子
5. 播放的音效要能夠停止

### 1 辨認使用者在鍵盤所按下的鍵

每一個按鍵都有對應的鍵碼(KeyCode)，所以我們可以透過鍵碼還得知使用者是按下哪一個按鍵。

在此[網站](http://keycode.info/)可以查看鍵碼。

![](https://i.imgur.com/QhZmc8W.png)

`addEventListener`：在 JS 中，要監聽事件的話通常會用到 `addEventListener`。在這裡也是，為了要監聽使用者按了哪個按鍵，我們會寫這樣子：

鍵盤，卷軸，螢幕旋轉大多都會做在`window`這個物件身上，所以監聽`window`物件。

```javascript=
window.addEventListener("keydown",playHandler)

function playHandler(e){
    console.log(e);
}
```

在這裡可以使用`keypress`或`keyup`。
需特別注意，使用`keypress`會出現`null`，在最後的延伸會紀錄這三者的差異。

函式的參數中會預設回傳一個屬於該事件引發後的物件，在這裡我們用 `console.log` 來看看它會回傳什麼事件。

![](https://i.imgur.com/E8qM1D0.png)

可以觀察到裏面包含了我們的`KeyCode`與`Key`。

### 2 鍵盤按下指定按鈕後能夠觸發音效

可以觀察到 HTML 的部分，都會帶一行`data-* attribute`，這裡它用的是 `data-key`。

![](https://i.imgur.com/CsjerB9.png)

`querySelector`：JS 原生 CSS 選擇器，需要注意的地方是，**若找不到相對應的元素會回傳 null，否則會回傳第一個符合的元素**。所以，如果是多個屬性具有相同的名稱時，他只會選擇到第一個符合的元素。

如果需要選取多個具有相同的 class 名稱的元素時，就需要使用`querySelectorAll`。

需注意的是在`querySelector()`裡面，使用了 ES6 中的模版語言。它是使用 ‵ 符號，在模版字串中如果有需要引入變數，則可以是用`${ }`，來代入變數。

```javascript=
function audioHandler(e){
const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
```

這邊的判斷式，是判斷如果按了不是指定的鍵，就透過`return`來停止這個函式。

如果是正確的鍵，則播放音樂。

`audio.currentTime = 0`，讓音樂每次播放都可以回到第 0 秒。

```javascript=
function audioHandler(e){
const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
if(audio){
  audio.play();
}
else{
  return ;
}
```

這邊會遇到一個問題，連續按下指定的鍵時，預期狀況是聲音會重複播放，但實際上並沒有。

而是斷斷續續的播，這是因為聲音長度為 3 秒。使用`.play()`時，音效還沒播放結束，所以他不會馬上執行。

解決這個問題的方法，就是每按下鍵時，讓音檔回到一開始，利用`currentTime`這個屬性。

```javascript=
function audioHandler(e){
const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
if(audio){
  audio.currentTime =0;
  audio.play();
}
else{
  return ;
}
```

### 3 鍵盤按下後，指定的按鍵出現動畫效果

處理完聲音的部分後，來處理按鍵動畫的部分。

當鍵盤按下特定按鍵，在`html`上加上特定的`class`，然後再移除。

和剛剛相同的，先監聽按鍵，然後取得按鍵所對應的網頁元素。

```javascript=
function playHandler(e){
  const dom = document.querySelector(`div[data-key="${e.keyCode}"]`);
}
```

可以觀察到原本套用在元素上的只有`.key`，在我們按下指定的按鈕以後，就會套用`.playing`這個屬性。

![](https://i.imgur.com/jXgcTAl.png)

`classList` 物件：當讓按下按鍵之後，能夠在該元素上添加指定的`class`以產生動態的效果，可以利用 JS 中內建的`element.classList.add( )`這個方法。

```javascript=
function playHandler(e){
  const dom = document.querySelector(`div[data-key="${e.keyCode}"]`);
  if (dom) dom.classList.add('playing');
}
```

加上`.play`之後會遇到的問題就是，該如何將它移除?

`transitionend event`：這個 `transitionend` 事件主要是對應到 css 中 `transition` 的動畫效果，當這個 `transition` 效果執行結束的時候會引發事件。

所以，監控每一個按鍵的 `transitionend event` ，一旦我們偵測到這個動畫效果已經結束，那麼我們就可以把原本添加的 `.playing` 這個 `class` 拿掉。

`querySelectorAll`：為了監聽每一個按鍵的事件，這裡我們就會用到 `querySelectorAll`這個方法，它會選出所有具有該 `class` 的元素，並回傳為 `NodeList`。

`forEach( )`：為了要重複的讀出這個`NodeList`的內容，我們會用到 forEach( ) 這個方法。

```javascript=
// 選出所有具有 .key 的元素，回傳成陣列
document.querySelectorAll(".key").forEach(function(key){
// 利用forEach方法讀取NodeList，並監聽每一個事件的transitionend事件
// 事件執行時會出發transitionHandler
    key.addEventListener("transitionend",transitionHandler)
 })
```

撰寫 transitionHandler 函式，先看看回傳的物件有什麼?

```javascript=
function transitionHandler(e){
  console.log(e);
}
```

![](https://i.imgur.com/KqYTgBF.png)

這些東西是甚麼呢？

我們可以在圖片中看到 `propertyName` 的地方分別有 `border-*-color`，`border-*-width`，另外還有一個 `transform`。

這些東西是當 `transition` 效果結束之後會回傳的內容。

在這裡我們就拿 `propertyName = transform` 這個來當判斷，當`transform` 出來（也就是 `transition` 結束時），把 `.playing` 這個 class 移除。

```javascript=
function transitionHandler(e){
    console.log(e);
    if(e.propertyName === "transform"){
      e.currentTarget.classList.remove("playing");
    }
}
```

## 完整 Code

```javascript=
  (function(){
    function playHandler(e){
      // play music

      const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
      if (audio){
        audio.currentTime =0;
        audio.play();
      }
      // dom style
      const dom = document.querySelector(`div[data-key="${e.keyCode}"]`);
      if (dom) dom.classList.add('playing');
    }
    function transitionHandler(e){
      console.log(e);
        if(e.propertyName === "transform"){
          e.currentTarget.classList.remove("playing");
        }
      }

    document.querySelectorAll(".key").forEach(function(key){
        key.addEventListener("transitionend",transitionHandler)
     })
    window.addEventListener("keydown",playHandler)
  })()
```

## 延伸學習

[keydown, keypress, keyup 的差異](https://hackmd.io/@PhoebeHo/SJseFQZv_)

[HTML 5 中的資料屬性（data-\* attribute）](https://hackmd.io/@PhoebeHo/BywgvpZP_)

## 參考網站

[比較 keydown, keypress, keyup 的差異. 在網頁的鍵盤事件操作有三種 keydown, keypress… | by Tommy | Medium](https://medium.com/@yitailin/%E6%AF%94%E8%BC%83-keydown-keypress-keyup-%E7%9A%84%E5%B7%AE%E7%95%B0-4e873ba17e81)

[[技術分享] 什麼是 HTML 5 中的資料屬性（data-\* attribute） ~ PJCHENder<br>那些沒告訴你的小細節](https://pjchender.blogspot.com/2017/01/html-5-data-attribute.html)

[[筆記] JavaScript ES6 中的模版字符串（template literals）和標籤模版（tagged template） ~ PJCHENder<br>那些沒告訴你的小細節](https://pjchender.blogspot.com/2017/01/javascript-es6-template-literalstagged.html)

[[筆記] JS30 系列：監聽按鍵事件及撥放音效（Day1） ~ PJCHENder<br>那些沒告訴你的小細節](https://pjchender.blogspot.com/2017/01/js30day1.html)
