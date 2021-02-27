---
title: "[實作] Georgia Restaurant"
author: Phoebe
tags: HTML&CSS
categories: Portfolio
date: 2021-02-26 11:07:11
---

這個實作有點難以做筆記，這邊的 code 都以 commit 的紀錄來解析，以記錄切版流程為主，方便以後自己實作可以參考。

## 建立 Header

<!--more-->

![](https://i.imgur.com/XXxAuyt.jpg)

### 第一步 建立 Header 架構

#### HTML

```html=
<header class="header">
    <div class="brand">
        <a href="#" class="logo"><i class="fas fa-utensils"></i></a>
        <div>
            <h1 class="main-name">Georgia</h1>
            <p class="sub-name">Restaurant</p>
        </div>
    </div>
    <div class="header-banner">
        <h1 class="main-heading">Welcome</h1>
        <h3 class="sub-heading">Try Great Georgia Dishes</h3>
        <button type="button" class="main-btn">Reservation</button>
    </div>
</header>
```

### 第二步 加上 Header style

調整 brand，logo，main-name，sub-name

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/6e35e34ba1ffc1f0c8f3c13ec052477057580cca)

這裡分成四個 SCSS 檔案

1. main.scss
2. \_base.scss
3. \_layout.scss
4. \_components.scss

#### main.scss

只@import 檔案

```scss=
@import "base";
@import "layout";
@import "components";
```

#### \_base.scss

每個檔案都會用到的東西放在 base 裡。

- 顏色變數
- 字體變數
- @mixin
- \*，body

#### \_layout.scss

設定大元素

- 設定 header

#### \_compoment.scss

設定大元素裡的小元素

- 設定 header 裡的 logo
- main-name
- sub-name

### 第三步 完成 Header Style

完成`header-banner`，`main-heading`，`sub-heading`，`main-btn的style`。

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/473ba52d9c6b79c9b04dae37a99c5636ee44b5f1)

將 9-12 行的 css( 圖二紅色為刪除部分 )，轉換成`@mixin`(圖一 base.scss)。

就可以直接在其他地方使用`@include`直接套用( 圖二綠色部分 )。

> base.scss 圖 1

![](https://i.imgur.com/k3xuvQe.png)

> layout.scss 圖 2

![](https://i.imgur.com/3PrX53G.png)

`background-color: transparent`，可以使 button 背景透明。

## 建立 About us

![](https://i.imgur.com/ZRBiqzi.png)

### 第一步 建立 About us 架構

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/4a0f780ab1d7402b77a022814fcb468423f5b90b)

#### 如何產生 \*\*\* 的樣子?

`<i class="fas fa-star-of-life star"></i>`，可以引入**星字號**，做一個 quote 的效果。

需要在一開始加上 fontawesome 的連結

```html=
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.5.0/css/all.css" integrity="sha384-B4dIYHKNBt8Bc12p+WXckhzcICo0wtJAoU8YZTY5qE0Id1GSseTk6S+L3BlXeVIU" crossorigin="anonymous">
```

### 第二步 調整 About us Style

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/e4a94826f6bb3a72d33adaa19e03714473011695?file-filters%5B%5D=.scss)

#### 如何讓第一行出現段落空格?

`&::first-letter`的技巧，可以讓第一行出現段落空格(綠色方塊)。

![](https://i.imgur.com/6PWnGdw.png)

#### 畫面如何分成兩塊(圖與文字)?

左邊 width 佔`60%`，右邊 width 佔`40%`。

```scss=
.description {
    font-family: $font-josefinSans;
    font-size: 25px;
    font-style: italic;
    color: $color-secondary;
    text-align: justify;

    &::first-letter {
        padding-left: 50px;
    }
}
```

## 建立 Gallery

![](https://i.imgur.com/YHxUAbi.jpg)

### 第一步 建立 Gallery 架構

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/3de571216d992624f7e175506daf2221c80aedcd?file-filters%5B%5D=)

結構會是直向的一張一張圖片

```html=
<section class="gallery">
    <div class="cards-wrapper">
        <div class="card">
            <div class="card-overlay">
                <h1 class="card-overlay-heading">Food Name</h1>
                <p class="card-overlay-paragraph">Price: $30.00</p>
                <button type="button" class="card-overlay-btn">Order Now</button>
            </div>
            <img src="images/gallery-img-1.jpeg" class="card-img">
        </div>
</section>
```

### 第二步 調整 Gallery Style

#### 如何讓直向的卡片三個三個排列?

先設定`.card`( 每一張卡片 )為`width: 33.3333%`，然後`.card-overlay`( 包住所有卡片 )為`flex-wrap: wrap`。

#### 如何防止圖片變形?

```scss=
object-fit: cover
```

#### 重複出現的 code?

在`-img`和`-overlay`都會使用到

```scss=
width:100%;
height:100%;
```

這時，可以使用 sass 方法`@extend`繼承。

1. 先使用`%`設定

```scss=
%fullSpace {
    width: 100%;
    height: 100%;
}
```

2. 再使用`@extend`繼承

```scss=
@extend %fullSpace
```

#### sass 怎麼增加變數?

紅色部分為舊的，綠色為新的。

利用`$`就可以宣告，特別注意，`upperspace`為全部都變大寫，`captilize`為第一個字母大寫而已。

![](https://i.imgur.com/6eS4hkb.png)

#### 如何做出從右邊出現的效果?

注意要加上`overflow:hidden`，才可以使遮罩全部都隱藏起來，要不然會無法成功。

預設為`left:-100%`，`:hover`之後，才變成`left:0`。

![](https://i.imgur.com/LpFzd7y.png)

在-overlay 加上`transition: left .9s ease-in`，做出慢慢出現的動畫效果。

## 建立 Footer

![](https://i.imgur.com/IirTWos.png)

### 第一步 建立 Footer 架構

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/95ad559b2adbb4c7f336354a50e4b274548e956c)

#### 如何出現 copy 符號?

![](https://i.imgur.com/pnoEHBe.png)

```html=
<ul class="social-media">
    <li class="social-media-item">
        <a href="#" class="social-media-link">
            <i class="fab fa-facebook-square"></i>
        </a>
    </li>
</ul>
```

### 第二步 調整 Footer Style

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/2980d29f488a2c1c04646280f2a48b736ae7462f?file-filters%5B%5D=.scss)

#### 如何讓每個 icon 中間留有空格?

使用`justify-content: space-between`，就可以做到。

#### 如何做出 media 排列的效果?

![](https://i.imgur.com/nANhx2F.png)

使用`ul`包住所有`li`，再取消掉`list-style`。

## 建立 navbar

### 第一步 建立 navbar 架構

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/ff295fb8e1d6dfd963a9f86588e2f5693f42cf86)

#### 如何建立 navbar 的三條線?

![](https://i.imgur.com/FJGCVTd.jpg)

新增`checkbox`，確保點擊的時候會產生作用。

`input`的 id 為`check`，`label`的`for`為`check`，當`hamburger-menu`被點擊時，`input`就會被打勾。

![](https://i.imgur.com/yECpS9y.png)

#### 如何把頁面分兩半?

![](https://i.imgur.com/SKZYwKr.png)

`.navbar-navigation`內分成

1. `.navbar-navigation-left`
2. `.navbar-navigation-right`

左邊放圖片，右邊放頁面的連結。一樣利用`<ul>`加上`<li>`裡面包超連結`<a>`。

![](https://i.imgur.com/mPf0SCR.png)

### 第二步 調整 Navbar Style

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/a775f79e835d8e068c9661d4676dc107b0518cfc?file-filters%5B%5D=.scss)

#### 如何產生產生背景的 layout?

![](https://i.imgur.com/EQWRMkA.png)

整個`.navbar`需要加上`z-index:200`，讓選單可以出現在整個頁面之上，要不然會出現在後方。

`&-left`需要加上`position:fixed`。不管滾輪如何做上下移動，他都會維持在原位，像是放大版的**蓋板廣告**。

![](https://i.imgur.com/1GGBxvM.png)

#### 照片如何疊加上去?

![](https://i.imgur.com/INwCuhP.png)

利用**百分比**定位就可以完成。

![](https://i.imgur.com/UyIV07H.png)

## 建立 hamburger menu

[Code 連結](https://github.com/hff2/My-Projects/pull/14/commits/57b39fe43b0e68a5181b6ca758f0158f25ba1c89?file-filters%5B%5D=.scss)

### 第一步 定位到頁面右上方

利用絕對定位`fixed`搭配`top`跟`right`定位，再利用`z-index`定位在右上方。

![](https://i.imgur.com/OfFQnor.png)

### 第二步 設定 hamburger menu

設定線條

![](https://i.imgur.com/Tf0SiJb.png)

### 第三步 調整 hamburger menu style

#### 如何讓 navbar 以彈跳的方式出現?

設定彈跳出現的動畫。

```sass=
transition: right .8s cubic-bezier(1, 0, 0, 1);
```

#### 如何點擊 hamburger menu 時就讓 navbar 出現?

因為 input 的 id 是 check，label 的 for 也是 check，所以，在按下 label 時，input 也會被打勾，可以產生連動效果。

![](https://i.imgur.com/VZEhWVo.png)

#### 如何讓 hamburger menu 旋轉?

使用`rotateZ`就可以旋轉

![](https://i.imgur.com/bBOF3yb.png)

#### 如何讓三條線呈現一個叉叉?

將第一條線和第三條線設定旋轉。

![](https://i.imgur.com/IMD7lTX.png)

旋轉後，還需要設定`transform-origin:right`，讓兩條線可以成功變成叉叉。

![](https://i.imgur.com/vwI4SYL.png)

#### 如何將 input button 隱藏起來?

在 html 後方加上 hidden 就可以執行。

![](https://i.imgur.com/l7eWbLn.png)

## 添加 RWD

先設定好全部的`1600px`，再來設定`1300px`，一步一步設定。

### Header

增加 media query

以下寫法為小於`1600px`，`font-size`調整為`50px`。

```sass=
@media(max-width: 1600px) {
    font-size: 50px;
    margin-bottom: 50px;
}
```

![](https://i.imgur.com/z3mItlE.png)

### About us

在寬度為`800px`的時候，將左邊的圖片設定為`none`。

![](https://i.imgur.com/N2xx3YL.png)

然後`width`設定為 100%，就可以佔滿整個螢幕。

![](https://i.imgur.com/Fibp7fE.png)

### Gallery

不想要其他資訊顯示時，就使用`display:none`

![](https://i.imgur.com/vZfmmSb.png)

### footer

使用`margin:auto`和`width:70%`置中。

![](https://i.imgur.com/BISq8ET.png)

### navbar

![](https://i.imgur.com/Dx8t4ip.png)

視窗過小時，左邊的圖片框就不出現。

所以設定為`width: 100vw`和`right: -100vw`(隱藏起來)。

![](https://i.imgur.com/vYYy8nB.png)

## 參考文章

[CSS 沒有極限 - Checkbox 的妙用](https://wcc723.github.io/css/2013/10/07/css-chechbox/)
