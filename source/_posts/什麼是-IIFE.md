---
title: 什麼是 IIFE?
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-01-24 09:20:02
---
## 當迴圈遇到`setTimeout()`

假設想透過迴圈 + `setTimeout()` 來做到，在五秒鐘之內，每秒鐘依序透過 console.log 印出： 0 1 2 3 4
<!--more-->
我們會直覺的寫下

```javascript=
for( var i = 0; i < 5; i++ ) {
  window.setTimeout(function() {
    console.log(i);
  }, 1000);
}
```
印出來的結果是5個5。

![](https://i.imgur.com/odKLnJ1.png)

為什麼不是1,2,3,4,5呢???

因為

JavaScript 是一個「非同步」的語言，所以當我們執行這段程式時， `for`迴圈並不會等待`window.setTimeout()`結束後才繼續。

而是在執行階段就一口氣就把他跑完。


所以`for`迴圈在開始執行的第一個瞬間(0的時候)，就把五次的`window.setTimeout()`跑完。然後跑到1時，全部把5印出來。



要如何避免這個問題呢?

![](https://i.imgur.com/RWhBoyW.png)

可以利用「切分變數有效範圍的最小單位是`function`」這個特性，把`window.setTimeout()`透過一個「立即被呼叫的特殊函式」來包裝。

像是這樣寫
```javascript=
(function(){
  // 做某事...
})();
```
下面來解釋這個這個神奇的寫法

1. 先加個小括號`()`把這個函式包起來

```javascript=
(function doSomething ( i ){
  // 做某事...
})
```
2. 因為要呼叫它，所以在後面再加個小括號 `()`

```javascript=
(function doSomething ( i ){
  // 做某事...
})(123)
```

3. 比對一下

> 一般呼叫函式
```javascript=
doSomething(123);
```
>函式宣告當下即呼叫

```javascript=
(function doSomething ( i ){
  // 做某事...
})(123);
```

可以很清楚的了解，立即函數，就如其名，它要馬上被執行。

## 解決`window.setTimeout`問題

回到`for`迴圈與`window.setTimeout`的問題。

```javascript=
for( var i = 0; i < 5; i++ ) {
  window.setTimeout(function() {
    console.log(i);
  }, 1000);
}
```

我們知道像上面這樣的寫法，在執行`window.setTimeout`的時候， `i`早已變成了5。

那麼為了可以保留每一次執行迴圈時，那個「當下的」`i`，我們可以用一個立即被呼叫的特殊函式將它包覆起來，然後將`i`作為參數傳入：

```javascript=
for( var i = 0; i < 5; i++ ) {
  (function(i){
    window.setTimeout(function() {
      console.log(i);
    }, 1000);
  })(i);
}
```

印出的結果就會是我們要的1,2,3,4,5

![](https://i.imgur.com/pQhWRWY.png)


## 封裝

廣義來說，IIFE也是儲存閉包的環境狀態的作法，在執行 `setTimeout()`的同時，會將當下的 i 鎖起來，延長它的生命。

在[Alex宅幹嘛的直播](https://www.youtube.com/watch?v=xeIbgAdEcUA&t=1838s&ab_channel=Alex%E5%AE%85%E5%B9%B9%E5%98%9B)裡，31.28s 有提到封裝的概念，寫Jquery第一件事情先處理scope，不處理的話`name`會被註冊在`window`上面，任何人都可以去讀取，使用，覆蓋我寫的資料。

以一般來說

```javascript=
<script>
//scope
var name = "Phoebe";
</script>
```

在開發人員工具可以直接讀取到name

![](https://i.imgur.com/ta8BtEd.png)

而scope就是開一個密閉的空間，寫在裡面，不給別人看到。

```javascript=
//scope
//IIFES
(function () {
    var Myname = "Phoebe";
})();

```
### 使用立即函式封裝

封裝後就讀取不到了

![](https://i.imgur.com/nzxZrdV.png)



## 參考文章

本筆記參考以下文章加上自己所理解出來的內容撰寫。

[重新認識 JavaScript: Day 18 Callback Function 與 IIFE](https://ithelp.ithome.com.tw/articles/10192739)