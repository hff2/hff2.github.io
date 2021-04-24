---
title: HTML 5 中的資料屬性（data-* attribute）
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-04-22 09:20:02
---

`data-* attribute` 這個東西很常出現，但卻常常搞不清楚他到底是什麼？

## 解釋屬性

<!--more-->

會有`data-* attribute`的出現，是因為在製作網頁的過程，我們會添加一些屬性名稱方便自己理解。

但是，不能每個人都定義自己的屬性名稱，為了要避免大家在 HTML 中隨意添加屬性，在 HTML5 中就多了 data-_ attribute 這個屬性。其中，`_`就是可以自定義的部分。

在使用 `data-* attribute` 時，\* 字號的地方不能包含大寫字母，也就是屬性名稱不能包含大寫字母，而屬性值則可以是任何的字串。

在 JS30 的 Day1 中，作者也有使用到了這個屬性。

```html=
<div data-key="65" class="key">
  <kbd>A</kbd>
  <span class="sound">clap</span>
</div>
<div data-key="83" class="key">
  <kbd>S</kbd>
  <span class="sound">hihat</span>
</div>
```

## 使用 JS 取得 data-\* attribute 的屬性值

當我們要取得 `data-* attribute`的屬性值時，我們可以簡單利用 JavaScript 中的 `dataset` 物件，就可以取得。

```javascript=
let key = document.querySelectorAll(".key");
console.log(key[0].dataset.key);
```
