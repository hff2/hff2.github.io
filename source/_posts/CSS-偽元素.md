---
title: CSS 偽元素
author: Phoebe
tags: HTML&CSS
categories: Web
date: 2021-01-30 00:56:50
---
## 什麼是「偽元素」？

「偽元素」之所以稱作「偽」，有兩個原因。

1. 從英文「Pseudo」翻譯過來
2. 因為它並不是真正網頁裡的元素，但行為與表現又和真正網頁元素一樣，也可以對其使用 CSS 操控。
<!--more-->
跟偽元素很像的還有**「偽類」**( Pseudo classes )。

在 W3C 的定義裡總共有五個偽元素，分別是`::before`、`::after`、`::first-line`、`::first-letter`和`::selection`。

為了區別偽類與偽元素，偽元素使用兩個冒號「`::`」開頭，而偽類使用一個冒號「`:`」開頭 ( 像是 `:hover` )。

## 偽元素 vs 偽類

| 種類 | 符號 | 比較 | 是否出現在DOM tree | 作用 |
| - | ------------- | ------------- |------------- |------------- |
| 偽類 | `:` | 不是元素 | 不會出現在 DOM tree | 用於定義元素的特殊狀態 |
| 偽元素 |`::` | 是元素 | 會出現在 DOM tree | 用於選擇元素的指定部分 |

DOM tree為**文件物件模型**。

## `::before` 與 `::after`


![](https://i.imgur.com/yQMeOLa.png)


`::before`、`::after` 是最常使用的偽元素，兩者都是以`display:inline-block`的屬性存在，`::before` 是在原本的元素**之前**加入內容。

`::after`則是在原本的元素**之後**加入內容，同時偽元素也會「**繼承**」原本元素的屬性，如果原本文字是黑色，偽元素的文字也會是黑色。

### 舉例來說

> 輸出：


![](https://i.imgur.com/ejt1CUE.png)

> 程式碼

```css=
    div::before {
      content: "I am before ";
      color: rgb(255, 163, 42);
    }
    div::after {
      content: " I am after";
      color: rgb(107, 107, 243);
    }
```

```html=
    <div>Hi,I am div.</div>
```




## 好用的 content

使用偽元素一定要具備 `content` 的屬性，就算是只有`content:"";`也可以，因為沒有 `content` 的偽元素是**不會出現在畫面上的**。然而，`content` 是個很特別的屬性，它可以使用 attr 直接獲取內容元素的屬性值 ( attribute )。

比如說，在 HTML 裡有一個超連結，點擊後會彈出新視窗並連結至 Google：

### 舉例來說

> 輸出：


![](https://i.imgur.com/m6Fk6sL.png)


> 程式碼

```css=
    a::before {
      content: attr(href);
      color: rgb(255, 163, 42);
    }
    a::after {
      content: attr(target);
      color: rgb(107, 107, 243);
    }
```
```html=
    <a href="https://www.google.com" target="_blank">google</a>
```




此外，`content` 內容是可以「**相加**」的，直接使用`空白鍵`就可以不斷的累加下去，以下面的程式碼來說，可以在剛剛擷取的超連結文字後方和 target 屬性前方，加入標點符號。

### 舉例來說

> 輸出：


![](https://i.imgur.com/bH9e1eZ.png)


> 程式碼

```css=
    a::before {
      content: "!" attr(href) "^";
      color: rgb(255, 163, 42);
    }
    a::after {
      content: "<" attr(target) ">";
      color: rgb(107, 107, 243);
    }
```

```html=
    <a href="https://www.google.com" target="_blank">google</a>
```


## 實際應用

### 偽類與偽元素 同時使用

> 輸出：


![](https://i.imgur.com/cptVBXk.png)

滑鼠移上去後

![](https://i.imgur.com/zaW5auy.png)

> 程式碼

```css=
    div:hover::after {
      content: " Change Color";
      color: rgb(255, 163, 42);
    }
    div::after {
      content: " Touch Me";
      color: rgb(107, 107, 243);
    }
```

```html=
    <div>Hello</div>
```


### 疊字效果

> 輸出：


![](https://i.imgur.com/Sf0X35x.png)

偽元素中搭配 `attr` ，可以從原本的 Element 獲取屬性的資料

> 程式碼

```css=
    .outBlock {
      position: relative;
    }

    .textBlock {
      position: absolute;
      top: 50px;
      left: 50px;
      font-size: 50px;
      font-weight: bold;
    }

    .textBlock::before {
      content: attr(data-content); /* 獲取資料 */
      position: absolute;
      top: -30px;
      height: 40px; /* 字體出現多少 */
      overflow: hidden;
      color: rgba(0, 0, 0, 0.7);
    }

    .textBlock::after {
      content: attr(data-content);
      position: absolute;
      top: -60px;
      height: 40px;
      left: 1px;
      overflow: hidden;
      color: rgba(0, 0, 0, 0.2);
    }
```

```html=
    <div class="outBlock">
      <div class="textBlock" data-content="HELLO">HELLO</div>
    </div>
```

可以從開發人員工具觀察到有`::after`與`::before`的屬性。

![](https://i.imgur.com/2lRV8lS.png)


## 參考文章

[CSS 偽元素 ( before 與 after )](https://www.oxxostudio.tw/articles/201706/pseudo-element-1.html)

[Day24：小事之 CSS 偽類 與 偽元素](https://ithelp.ithome.com.tw/articles/10196924)

[CSS | 全都是假的！關於那些偽類和偽元素 - 基本用法](https://medium.com/enjoy-life-enjoy-coding/css-%E5%85%A8%E9%83%BD%E6%98%AF%E5%81%87%E7%9A%84-%E9%97%9C%E6%96%BC%E9%82%A3%E4%BA%9B%E5%81%BD%E9%A1%9E%E5%92%8C%E5%81%BD%E5%85%83%E7%B4%A0-%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-4de48feb8607)