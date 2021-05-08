---
title: CSS Diner
author: Phoebe
tags: HTML&CSS
categories: Web
date: 2021-05-08 00:56:50
---

## 介紹

CSS Diner 是一個**輸入選擇器**來破關的小遊戲，前一陣子再學習其他技術，一段時間沒使用 css 語法後，就忘記了許多，推薦大家可以來這邊練習。

這邊會記錄我觀念不熟，或是不知道該如何解決關卡!

[CSS Diner - Where we feast on CSS Selectors!](https://flukeout.github.io/)

<!--more-->

## 1 ~ 10 關

### 第 4 關

後裔選擇器 Descendant Selector。

要選擇元素裡的元素 `A` `B`。要選擇`B`的話，就需要在`A`和`B`中空一格 `A B`。

以下方程式碼來說，要選擇到`<plate>`裡面的`<apple>`，就需要寫 `plate apple`。

```html=
<div class="table">
    <bento />
    <plate>
        <apple />
    </plate>
    <apple />
</div>
```

### 第 7 關

Class 選取器，`A.className`。

舉例來說，`ul.important` 選取所有 `<ul>` 帶有 `class="important"`的元素。

`#big.wide` 選擇所有元素帶有 `id="big"` 與`class="wide"`的。

這關想選取小的橘色，解法為`orange.small`。

```html=
<div class="table">
    <apple />
    <apple class="small" />
    <bento>
        <orange class="small" />
    </bento>
    <plate>
        <orange />
    </plate>
    <plate>
        <orange class="small" />
    </plate>
</div>
```

### 第 10 關

全體選擇器，Universal Selector。

使用 `*`，就可以選到畫面中的所有元素。

### 第 11 關

全體選擇器，Combine the Universal Selector 。

舉例來說，`p *` 選擇所有 `p` 裡面的元素。

`ul.fancy *`，選擇所有 `<ul class="fancy">` 裡面的元素。**注意中間要有空格**。

以下想選取 `<plate>` 裡的元素，就可以使用`plate *`。

```html=
<div class="table">
    <plate id="fancy">
        <orange class="small" />
    </plate>
    <plate>
        <pickle />
    </plate>
    <apple class="small" />
    <plate>
        <apple />
    </plate>
</div>
```

### 第 12 關
