---
title: Sass的基本用法
author: Phoebe
date: 2021-2-22 11:32:46
tags: HTML&CSS
categories: Web
---

## 1 設定變數

利用`$`**設定變數**，像是`$primary`，`$big-font:4rem`。

![](https://i.imgur.com/syZP7s0.png)
<!--more-->
```scss=
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
}

$primary : #a1a3c2;
$big-font:4rem;

section h2{
  color: $primary;
  font-size: $big-font;
}

section button{
  color: $primary;
}
```

## 2 嵌套 Nested Rules

解決 CSS 編寫過程中，**父元素重複編寫問題**，可以縮短開發流程。


這邊可以觀察到將h2，還有button寫在`.introduction`裡面，就是一種Nested，減少父元素重複編寫的問題。



```scss=
.introduction{
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  
  h2{
    font-size: $big-font;
  }
  
  button{
    border:none;
    background:$primary;
    padding: 1rem 3rem;
    cursor: pointer;
    transition: all 1s ease; //滑鼠漸變的效果
  }
}
```

也可以減少font的寫法

```scss=
.main {
    font: {
        family: Helvetica, sans-serif;
        size: 15em;
        weight: bold;
    }
}
```

## 3 引用父選擇器 &

如果想在嵌套狀態下，取得外層的父選擇器，可以使用「＆」，會直接**抓取父選擇器**。

常會把它用在，如 CSS 元件狀態：

`:hover`、`:focus`、`:hover`、`:link`、`:visited`、`:before`、`:after` 

```scss=
.introduction{
  min-height: 100vh;
  flex-direction: column;
  h2{
    font-size: $big-font;
  }
  button{
    cursor: pointer;
    &:hover{
      background-color: #555eda;
    }
  }
}
```

## 4 變量

在實際編寫 CSS 的過程中，常會遇到多次相同的顏色、字型、字體大小等 .. 重複出現。

SASS 中使用`$`進行宣告變數，支持7種主要數據類型：

1. 數字（如：1, 1.5, 20px）
2. 字符串，帶引號和不帶引號（如："foo", 'foo', foo）
3. 顏色（如：red, #28b0b4, rgba(0, 0, 0, 0.5)）
4. 布爾值（如： true, false）
5. 空值（如： null）
6. 值列表（list），用空格或逗號分開（如：2em 1em 0 1em、 Helvetica, Arial）
7. maps：一對 key 和 value（如：(key1: value1, key2: value2)）

```scss=
$bnr-font: Helvetica, sans-serif;
$bnr-color: #494947;

.banner1 p{
    font-family: $bnr-font;
    color: $bnr-color;
    padding: 10px 15px;
    letter-spacing: 0.2em;
}
.banner2 p{
    font-family: $bnr-font;
    color: $bnr-color;
    margin: 15px;
}
```

## 5 引入`@import` 

SASS 擴展了 CSS 的 `@import` 功能，允許在文件內導入其他的 SASS 或 SCSS 子文件。

在文件進行編譯後，被導入的 SASS 或 SCSS 子文件，會**全部合併到同一個CSS文件**，然後呈現出來。

把_footer.scss導入到style.scss。

```scss=
/** _footer.scss **/ 
footer{
  min-height: 10vh;
  h4{
    font-size: 2rem;
  }
}
```

使用`import`引入

```scss=
@import 'global';
@import 'intro';
@import 'footer';
```

## 6 混合`@mixin`和`@include`

若是有重複的代碼，會**不斷使用到**，就可用混合指令（Mixin Directives）

- 使用 `@mixin` 定義一個「 混合 」
- 使用 `@include` 引用一個「 混合 」
- 可同時引用多個「 混合 」

```scss=
@mixin font-main {
    font: {
      family: Arial;
      size: 16px;
      weight: 100;
    }
    color: #000;
}

/** 引用 mixin **/
.box p {
    @include font-main;
}
```

## 7 繼承`@extend`

若想讓多個 class 使用相同樣式，就可使用 @extend 直接繼承過來，減少重複編寫的時間。

```scss=
%msg-style {
    display: block;
    flex-wrap: wrap;
    background: #d9d9d8;
    color: #000;
}

.msg {
    @extend %msg-style;
}

.msg-success {
    @extend %msg-style;
    background: #34fc6d;
}

.msg-error {
    @extend %msg-style;
    background: #fc253e;
}
```


## 參考文章

[SASS教學 ＋SCSS：CSS 再進化，掌握語法攻略！](https://frankknow.com/sass-tutorial/#subject-4)


[新手也可以輕鬆玩轉 SASS - @mixin and @include](https://5xruby.tw/posts/play-sass-mixin-and-include/)