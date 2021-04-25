---
title: "Bootstrap 5 格線系統筆記"
author: Phoebe
tags: Bootstrap
categories: Bootstrap
date: 2021-03-8 11:07:11
---

## Bootstrap5 快速簡介

<!--more-->

明明有第一手的資訊為什麼還要看二手的?

學習看第一手的資訊，獲得最正確的觀念。

## Bootstrap5 安裝與快速檢測方式

### 第一種: 預設的 template

使用 CDN 連結的方式

[Bootstrap5 的首頁](https://getbootstrap.com/docs/5.0/getting-started/introduction/#starter-template)

![](https://i.imgur.com/b0RrZ0O.png)

> 使用網路服務的樣板

```html=
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-BmbxuPwQa2lc/FVzBcNJ7UAyJxM6wuqIj61tLrc4wSX0szH/Ev+nYRRuWlolflfl" crossorigin="anonymous">

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>

    <!-- Optional JavaScript; choose one of the two! -->

    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/js/bootstrap.bundle.min.js" integrity="sha384-b5kHyXgcpbZJO/tY9Ul7kGkf1S0CWuKcCD38l8YkeH8z8QjE0GmW1gYU5S9FOnJ0" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.6.0/dist/umd/popper.min.js" integrity="sha384-KsvD1yqQ1/1+IA7gi3P0tyJcT3vR+NdBTt13hSJ2lnve8agRGXTTyNaBYmCR/Nwi" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta2/dist/js/bootstrap.min.js" integrity="sha384-nsg8ua9HAw1y0W1btsyWgBklPnCUAFLuTMS2G72MMONqmOymq585AcH49TLBQObG" crossorigin="anonymous"></script>
    -->
  </body>
</html>
```

### 第二種: 下載到本地端

不同的開發模式，會有不同的安全性問題需要考量，有些採用把檔案下載到**本地端**，較為安全，因為別人無法輕易的更改這些檔案。

`popper.min.js` 為第三方的文件，並不屬於 Bootstrap。

要放入的檔案為:

1. bootstrap.min.js
2. [popper.min.js](https://cdn.jsdelivr.net/npm/@popperjs/core@2.6.0/dist/umd/popper.min.js)
3. bootstrap.min.css

Layout 裡面的 grid 是 bootstrap 採用 `flex` 做出來的格線系統，會稱為**系統**是因為它是有規則存在。

---

格線系統是將**空間**分割成 12 欄，分割成**12 等分**。

![](https://i.imgur.com/BOYoDCH.png)

`.container`，是一個定寬容器。(有固定的寬度，並且在不同的裝置會有不同的寬度)

`.container-fluid`，沒有固定寬度，預設就是滿版。

#### `.container`與`.container-fluid`的差異?

如果是用平板觀看網頁，`.container`就會在頁面旁邊有空間。

而`.container-fluid`就會呈現滿版的樣子，看起來會比較壓迫。

[格線系統範例](https://codepen.io/phoebe-ho/pen/WNoXorJ)

## Bootstrap5 格線系統入門

### 格線自動分欄 `col`

格線自動分欄，如果要做 5 個`item`在同一行要如何做?

這邊的疑慮為，空間分割成 12 個欄，出現**奇數**時，會無法除盡。

> 解決方法

直接使用五個`col`即可，因為格線系統會**自動分欄**，要幾欄有幾欄，寬度會自動決定。

![](https://i.imgur.com/lOIs67g.png)

```html=
<div class="container">
    <div class="row">
        <!-- 1 -->
        <div class="col">
            <div class="item">
                <img src='https://picsum.photos/300/200?random=10' class="w-100">
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
            </div>
        </div>
        <!-- 2 -->
        <div class="col">
            <div class="item">
                <img src='https://picsum.photos/300/200?random=15' class="w-100">
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
            </div>
        </div>
        <!-- 3 -->
        <div class="col">
            <div class="item">
                <img src='https://picsum.photos/300/200?random=20' class="w-100">
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
            </div>
        </div>
        <!-- 4 -->
        <div class="col">
            <div class="item">
                <img src='https://picsum.photos/300/200?random=20' class="w-100">
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
            </div>
        </div>
        <!-- 5 -->
        <div class="col">
            <div class="item">
                <img src='https://picsum.photos/300/200?random=20' class="w-100">
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
            </div>
        </div>
    </div>
</div>
```

### 固定寬度的格線用法 `col-4`

格線系統是將空間分割成 12 欄，分割成 12 等分。

所以假如要放 3 個 column，就使用 12/4=3，`col-4`，4 為三個 div 各獲得 4 個空間。

![](https://i.imgur.com/XCTaP4j.png)

```html=
<!-- 每一個元素佔12/4=3格 -->
<div class="col-4">
    <div class="item">
        <img src='https://picsum.photos/300/200?random=10' class="w-100">
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
    </div>
</div>
<div class="col-4">
    <div class="item">
        <!-- w-100 寬度100% -->
        <img src='https://picsum.photos/300/200?random=15' class="w-100">
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
    </div>
</div>
<div class="col-4">
    <div class="item">
        <img src='https://picsum.photos/300/200?random=20' class="w-100">
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
    </div>
</div>
```

### Breakpoint

[Breakpoints · Bootstrap v5.0](https://getbootstrap.com/docs/5.0/layout/breakpoints/)

> 小於 574px，螢幕解析度小於 576px 就會生效

- 小於 576px，最小型的裝置。
- 大於等於 576px，手機的橫向。
- 大於等於 768px，平板的直向。
- 大於等於 992px，平板的橫向(較舊的裝置，新的為 1024px)。
- 大於等於 1200px，平板的橫向(ipad pro)。
- 大於等於 1400px，Bootstrap5 增加的。

![](https://i.imgur.com/GJkUXSb.png)

### Container

[Containers · Bootstrap v5.0](https://getbootstrap.com/docs/5.0/layout/containers/)

`.container`旁邊都會留空間，讓畫面更好觀看。

![](https://i.imgur.com/0KiCLZU.png)

### .row 做了什麼事情

1. `display flex` 做出幾欄幾欄的欄寬，可以進行橫向排列。
2. `flex wrap` 格線可以做換列。
3. `margin-left/right`的負值，`container`會有左右的`padding`，把它抵銷掉，可以占滿空間。

### 格線在不同尺寸的應用

在手機為 12 欄，在 768px 以上的裝置為 4 欄，在 992px 以上為 3 欄，在 1400px 桌機上為 6 欄。

```html=
<div class="col-12 col-md-4 col-lg-3 col-xxl-2">
    <div class="item">
        <img src='https://picsum.photos/300/200?random=65' class="w-100">
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
    </div>
</div>
```

### 自動欄寬 RWD 應用

全部設定為只有 col。

直接在 row 上面動手腳，一樣可以達到效果。

```html=
<div class="row row-cols-md-3 row-cols-lg-4 row-cols-xxl-6">
<!-- col在不同的裝置上面，有不同的設定，不同的欄寬數。 -->
<!-- 希望在平板上面有作用 -->
<div class="col-md">
    <div class="item">
        <img src='https://picsum.photos/300/200?random=10' class="w-100">
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
    </div>
</div>
```

### 控制欄位的間距

`g-`為欄中間的間距，也可以設定`g-0`，就不會有空間。

```html=
<div class="g-5 row row-cols-md-3 row-cols-lg-4 row-cols-xxl-6">
    <div class="col-md">
        <div class="item">
            <img src='https://picsum.photos/300/200?random=10' class="w-100">
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas corrupti, delectus minima ipsum ipsam laborum vero deleniti sint recusandae? Et libero ea beatae quod est dolorum hic excepturi totam exercitationem?</p>
        </div>
    </div>
</div>
```

## Bootstrap 格線對齊與分布

### 放三個 column，卻要置中該如何做?

使用`col-3`卻只有 3 個`div`，會導致`div`偏左，右邊空了一格`col`。

解決方法可以使用，`justify-content-center`與`align-items-center`對齊。

---

![](https://i.imgur.com/1YiCxQ3.png)

在`row`裡使用`justify-content-around`，跟純 CSS 比較起來，差在語法裡不用寫重複的`flex`。

```html=
<div class="container">
    <!-- 在這裡加入justify-content-around -->
    <div class="row justify-content-around">
        <div class="col-12 col-md-3">
            <div class="item">
                <img src='https://picsum.photos/300/200?random=20' class="w-100">
                <h3>title</h3>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure, nihil!</p>
            </div>
        </div>
        <div class="col-12 col-md-3">
            <div class="item">
                <img src='https://picsum.photos/300/200?random=25' class="w-100">
                <h3>title</h3>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure, nihil!</p>
            </div>
        </div>
        <div class="col-12 col-md-3">
            <div class="item">
                <img src='https://picsum.photos/300/200?random=30' class="w-100">
                <h3>title</h3>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure, nihil!</p>
            </div>
        </div>
    </div>
</div>
```

---

### 文字放到畫面正中央

在`row`上面使用`justify-content-center`與`align-items-center`。

![](https://i.imgur.com/DuQDyyP.png)

kv = key version

使用`align-items-center`**沒效果**時，可能是`.container`與`.row`未設定高度的問題，所以在後面設置`h-100`即可。

```html=
<div class="kv">
    <div class="container h-100">
        <div class="row justify-content-center align-items-center h-100">
            <div class="col-8 col-md-6">
                <div class="text">
                    <h1>金魚都能懂得Bootstrap</h1>
                    <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Delectus, suscipit.</p>
                </div>
            </div>
        </div>
    </div>
</div>
```

## 格線排序控制

[Order · Bootstrap v5.0](https://getbootstrap.com/docs/5.0/utilities/flex/#order)

### Order 的使用方法 1

`order-last`，order 設定相同時(都有設定時)，按照原始碼的順序，A 前 B 後。

![](https://i.imgur.com/4jcyoEG.png)

> order 要設定在誰身上?

`item`外面的`div`，同`col`元素。

```html=
<div class="container">
  <div class="row">
    <!-- order-last-->
    <div class="col-3 order-last">
      <div class="item">A Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <!-- order-last-->
    <div class="col-3 order-last">
    <div class="item">B Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
  </div>
    <div class="col-3">
      <div class="item">C Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-3">
      <div class="item">D Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
  </div>
</div>
```

### Order 的使用方法 2

`order-順序`，直接指定排序。

![](https://i.imgur.com/qoHaWOh.png)

```html=
<div class="row">
<!-- order-順序 -->
    <div class="col-3 order-3">
        <div class="item">A Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-3 order-4">
        <div class="item">B Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-3 order-2">
      <div class="item">C Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-3 order-1">
      <div class="item">D Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
</div>
```

### Order 的使用方法 3

`order-first`，指定順序。

```html=
<div class="container">
  <div class="row">
    <div class="col-3">
      <div class="item">A Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-3 "
    ><div class="item">B Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
  </div>
    <div class="col-3 order-first">
      <div class="item">C Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-3 order-first">
      <div class="item">D Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
  </div>
</div>
```

### Order 的使用方法 4

預設的`order`值為 0，所以只要大於 0，就會往後面排列。

與`order-last`使用方法相同。

```html=
<div class="container">
  <div class="row">
    <!--  order-1往後排  -->
    <div class="col-3 order-1">
      <div class="item">A Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-3 order-1"
    ><div class="item">B Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
  </div>
    <div class="col-3">
      <div class="item">C Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-3">
      <div class="item">D Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
  </div>
</div>
```

### 在不同裝置呈現不同排序

`mb-4`為`margin-bottom`。

`order-md-1`，可以控制在特定裝置的排序。

```html=
<div class="container">
  <div class="row">
    <div class="col-12 col-md-3 mb-4 order-md-1">
      <div class="item h-100">A Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-12 col-md-3 mb-4 order-md-3"
    ><div class="item h-100">B Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
  </div>
    <div class="col-12 col-md-3 mb-4 order-md-2">
      <div class="item h-100">C Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-12 col-md-3 mb-4 order-md-4">
      <div class="item h-100">D Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
  </div>
</div>
```

與上述方法效果相同

使用`order-md-last`

```html=
<div class="container">
  <div class="row">
    <div class="col-12 col-md-3 mb-4">
      <div class="item h-100">A Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-12 col-md-3 mb-4 order-md-last"
    ><div class="item h-100">B Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
  </div>
    <div class="col-12 col-md-3 mb-4">
      <div class="item h-100">C Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
    <div class="col-12 col-md-3 mb-4 order-md-last">
      <div class="item h-100">D Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae porro incidunt molestias consectetur eaque, enim distinctio voluptatem cumque! Cumque, repudiandae!</div>
    </div>
  </div>
</div>
```

## `offset`格線距離控制

[Columns · Bootstrap v5.0](https://getbootstrap.com/docs/5.0/layout/columns/#offsetting-columns)

![](https://i.imgur.com/9kHdEqg.png)

旁邊少一格的狀況，可以使用`offset`進行調整。

`offset`的使用主要為：將元素推向右方。實際為，原本的空間再加上其他空間的意思。

已下方圖為例，`col-4`+`offset-4`就會變成 8，於是就將`div`推過去了。

![](https://i.imgur.com/jW0AZdf.png)

---

### 如何做出交錯的版?

![](https://i.imgur.com/x07JOHU.png)

1. 設定`col-md-7`，讓元素變成兩行。
2. 再將文字 div 設定`offset-md-5`，往右推五個欄位。

需要設定`md`，讓它**平板以上**才吃到這個設定，要不然手機版面會跑版!

```html=
<div class="col-12 col-md-7">
    <div class="pic">
        <img src='https://picsum.photos/300/200?random=25' class="w-100">
    </div>
</div>
<!-- offset-md-5，推過去5欄。 -->
<div class="col-12 col-md-7 offset-md-5 txt-block">
    <div class="txt">
        <h2>title</h2>
        <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Id cupiditate ipsam nihil voluptatem nisi odit dolorem architecto, molestias atque, corporis non laudantium consectetur quisquam eum, est dicta debitis accusantium? Laudantium!</p>
    </div>
</div>
```

交錯方法同上。

![](https://i.imgur.com/sGE0Mgi.png)

```html=
<div class="col-12 col-md-7 mt-5 offset-md-5">
    <div class="pic">
        <img src='https://picsum.photos/300/200?random=55' class="w-100">
    </div>
</div>
<!--  -->
<div class="col-12 col-md-7 txt-block">
    <div class="txt">
        <h2>title</h2>
        <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Id cupiditate ipsam nihil voluptatem nisi odit dolorem architecto, molestias atque, corporis non laudantium consectetur quisquam eum, est dicta debitis accusantium? Laudantium!</p>
    </div>
</div>
```
