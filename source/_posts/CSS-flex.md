---
title: CSS flex
author: Phoebe
tags: HTML&CSS
categories: Web
date: 2021-02-23 00:56:50
---
### 前言

flex 可以控制比例縮減分配，也能夠控制膨脹、縮減，順序。

[參考範例](https://codepen.io/frank890417/pen/ayLvRp)

### 1. 先設定flex排版
<!--more-->
```css=
.container{
  display:flex
}
```

### 2. 設定排版方向 `flex-direction`

預設是`row`

[flex-direction](https://www.w3schools.com/cssref/playit.asp?filename=playcss_flex-direction) 效果預覽。

```css=
.container {
  display: flex;
  flex-direction: row|row-reverse|column|column-reverse|initial|inherit;
}
```
### 3. 元素超出螢幕範圍時是否換行 `flex-wrap`

視窗縮小時，不會被強行擠壓，自動換行。

[flex-wrap](https://www.w3schools.com/cssref/playit.asp?filename=playcss_flex-wrap) 預覽效果

```css=
.container {
  display: flex;
  flex-wrap: nowrap|wrap|wrap-reverse|initial|inherit;
}
```

### 4. direction 和 wrap 二合一 `flex-flow`

用flex-flow可以只寫一行，就把direction 和 wrap 二合一。

第一個參數direction，第二個是wrap。

```css=
.container {
  display: flex;
  flex-flow:row-reverse nowrap;
}
```

### 5.元素對齊的方式之一 `justify-content`

`justify-content`是元素對齊的方式

是一種**水平排版**的方式，但會隨著主軸和副軸產生變化。

[justify-content](https://www.w3schools.com/cssref/playit.asp?filename=playcss_justify-content) 效果預覽

```css=
.container {
  display: flex;
  justify-content: flex-start|flex-end|center|space-between|space-around|initial|inherit;
}
```

### 6.元素對齊的方式之二 `align-items`

`align-items`是元素對齊的方式

是一種**垂直置中**的方式，但會隨著主軸和副軸產生變化。

[align-items](https://www.w3schools.com/cssref/playit.asp?filename=playcss_align-items) 效果預覽

```css=
.container {
  display: flex;
  align-items: stretch|center|flex-start|flex-end|baseline|initial|inherit;
}
```
### 7.多行元素對齊的方式 `align-content`

align-content是**多行元素對齊**的方式。

[align-content](https://www.w3schools.com/cssref/playit.asp?filename=playcss_align-content) 效果預覽

```css=
.container {
  display: flex;
  align-content: stretch|center|flex-start|flex-end|baseline|initial|inherit;
}
```

## CSS Flex個別子元素的排版

### 1.個別子元素的對齊 – align-self

`align-self`是針對個別子元素的對齊調整，外層需要是flex。

[align-self](https://www.w3schools.com/cssref/playit.asp?filename=playcss_align-self) 效果預覽

```css=
.container {
  display: flex;
}

.div { 
  align-self: auto|stretch|center|flex-start|flex-end|baseline|initial|inherit;
}
```

### 2.個別子元素的寬度 – flex-grow & flex-shrink

字面上的意思就是增加與減少，針對個別子元素的寬度調整。


[flex-grow](https://www.w3schools.com/cssref/playit.asp?filename=playcss_flex-grow) 效果預覽

[flex-shrink](https://www.w3schools.com/cssref/playit.asp?filename=playcss_flex-shrink) 效果預覽

```css=
.container {
  display: flex;
}

.div { 
  flex-shrink:8;
}

.div2 {
  flex-grow:8;
}
```

### 3. 最基本的寬度 `flex-basis`

`flex-grow`不能使`flex-wrap`功能運行，會**無法跳行**。

但是，只要設定了`flex-basis`之後可以換行。假如設定`flex-basis`為10rem，只要視窗讓方框小於10rem，它就會換行。

flex-basis有點像是最基本(最小)的寬度。

[flex-basis](https://www.w3schools.com/cssref/playit.asp?filename=playcss_flex-basis) 效果預覽

[flex 實際練習](https://codepen.io/phoebe-ho/pen/ExgWqeB)