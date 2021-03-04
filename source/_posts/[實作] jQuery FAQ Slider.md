---
title: "[實作] jQuery FAQ Slider"
author: Phoebe
tags: Javascript
categories: Portfolio
date: 2021-03-2 11:07:11
---

## 學習到的知識點

### Jquery

- slideToggle
- siblings
<!--more-->
- slideUp
- children
- not
- toggleClass

## 簡介

[Demo](https://hff2.github.io/My-Projects/Faq_Slider/index.html)

學習使用 Jquery UI 的[Accordion](https://jqueryui.com/accordion/)如何使用。

![](https://i.imgur.com/jfCO8FF.png)

## HTML

### 結構

使用`<ul>`和`<li>`實作。

```html=
<div id="container">
    <h1>jQuery FAQ Slider</h1>
    <div class="title">
        <h3>FAQ Slider Using jQuery</h3>
    </div>
    <ul class="faq">
        <!-- 1 -->
        <li class="q"><img src="./img/arrow.png">
            Lorem ipsum dolor sit amet consectetur adipisicing elit deleniti?
        </li>
        <li class="a">
            soluta ut blanditiis illo quisquam id consequatur dolor ipsam ipsa?
        </li>
</div>
```

## CSS

[完整 Code](https://github.com/hff2/My-Projects/blob/faq-slider/Faq_Slider/css/style.css)

### 如何讓 answer 一開始不出現?

使用`display:none`預設為不出現。

```css=
.faq li.a{
    background: #ddd;
    display: none;
}
```

### 點擊 Question 時，img 如何出現翻轉?

```css=
.rotate{
    -webkit-transform: rotate(90deg);
    -moz-transform: rotate(90deg);
    transform: rotate(90deg);
}
```

## JS

### 如何讓 Answer 出現?

![](https://i.imgur.com/Fazl8hr.png)

這邊使用了**鍊式**的技巧。

1. 當`class="q"`被`click`的時候，他的`next()`也就是`class="a"`，

![](https://i.imgur.com/JSRJvxb.png)

2. 使用`slideToggle`就可以產生上下收起的效果

3. `siblings`選取到同父元素的所有其他元素。

4. `slideUp`向上滑動

```javascript=
var action = "click";
var speed="500";

$(document).ready(function () {
    //Question handler
    $("li.q").on(action,function(){
        // Get next element
        $(this).next()
            .slideToggle(speed)
                // Select all other answers
                .siblings("li.a")
                    .slideUp();
    });
});
```

### 怎麼樣讓箭頭在點擊時 90 度旋轉?

1. `children`是返回所有子元素(父元素為`li.q`)，所以裡面的 img 會被選取到。

2. `.not`刪除所有符合表達式條件的元素。只要不是`img`的，都要去除掉`.rotate`。

3. `.toggleClass`可以進行**設置與移除**的切換。

```javascript=
//Get image for active question
var img = $(this).children('img');

//Remove the 'rotate' class for all images except the active
$('img').not(img).removeClass('rotate');

// Toggle rotate class
img.toggleClass('rotate');
```

## 參考文章

[Jquery 中 next()方法與 prev()方法的使有和詳解](https://www.itread01.com/content/1549818083.html)

[.slideToggle()](https://api.jquery.com/slidetoggle/)

[jQuery siblings() 方法](http://www.w3big.com/zh-TW/jquery/traversing-siblings.html)

[jQuery 篩選元素 (Traversing)](https://www.fooish.com/jquery/traversing.html)
