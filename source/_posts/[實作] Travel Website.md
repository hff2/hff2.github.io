---
title: '[實作] Travel Website'
author: Phoebe
tags: HTML&CSS
categories: Portfolio
date: 2021-02-07 11:07:11
---
## 前置 Settings
### HTML

在meta裡面加入一些東西

```html=
<meta
  name="description"
  content="Travelly is a travel agency website that helps you pick out your holiday vacation"
/>
<meta name="robots" content="index,follow" />

```
<!--more-->
加入頁面標籤的icon
```html=
<link rel="icon" href="icons/plane.svg" />
```

### CSS

font-size: 62.5%，1rem will be 10px。


各瀏覽器預設字型字號為**16px**，16px相當於1rem。

當我們定義 10px / 16px = 0.625 = 62.5% 時，瀏覽器的預設字型為16px * 62.5% = 10px。

此時，10px相當於1rem。

```css=
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  /* 1rem will be 10px */
  font-size: 62.5%;
}
```

## Creating Our Nav&Hero

![](https://i.imgur.com/ngnMpS9.jpg)

<!--more-->
### Header Html
超連結使點選標題時，直接到頁面的該位置。

```html=
<header class="main-head">
  <nav>
    <h1 id="logo"><a href="#hero">Travelly</a></h1>
    <ul>
      <li><a href="#locations">Location</a></li>
      <li><a href="#benefits">Benefits</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</header>
```

### Section Hero

```html=
<section id="hero">
  <h2>Travel Beyond Limits.</h2>
  <h3>
    Start your travel at an affordable price with Travelly<br />Contact us
    now bellow.
  </h3>
  <button>Book now</button>
</section>
```

### Header Css

1. nav bar會隨著視窗做變化，但我們希望nav bar不要隨著視窗做變化時，可以使用`padding`+`min-height`代替。
2. 要讓整個頁面的兩邊保持空間，`width: 90%`， `margin: auto`。

![](https://i.imgur.com/U7LMA6s.png)

3. `flex: 1 1 40rem`，flex: grow shrink basis。`flex-grow`不長大，`flex-shrink`不縮小，`flex-basis`基本標準。

4. 直接套給logo的字體,`font-weight`可以在下載字體時設定。

```css=
#logo{  
  font-family: "Pattaya", sans-serif;
  font-weight: 400;
}
```
5. `flex-wrap:wrap`，nav的標籤會自動Jump Down。[什麼是flex wrap](https://hff2.github.io/2021/02/23/CSS-flex/)

![](https://i.imgur.com/7ksrvwj.png)

6. `flex: 1 1 40rem;`，只要視窗空間小於40rem，就會馬上Jump Down。

7. 讓nav bar保持在上方，`position: sticky;`，`top: 0;`，`z-index: 3;`

```css=
h1 {
  font-size: 2.6rem;
}
li,
button,
label,
input,
p {
  font-size: 2rem;
}

h2 {
  font-size: 4.8rem;
}
h3 {
  font-size: 3rem;
  font-weight: normal;
}

h4,
h5 {
  font-size: 2.8rem;
}

a {
  color: white;
  text-decoration: none;
}


/* Nav Section With Hero */
/* 改變header的背景色 */
.main-head {
  background-color: #131c17;
  color: white;
  /*  讓nav bar保持在上方  */
  position: sticky;
  top: 0;
  /* 被雲擋住，所以加上z-index:3 */
  z-index: 3;
}

/* PARENT */
nav {
  /* 會隨著視窗做變化，
  /* min-height: 10vh; */
  display: flex;
  /* 讓整頁面的兩邊都可以留下內縮的空白 */
  width: 90%;
  margin: auto;
  /* 如果沒有padding，nav不會隨著視窗縮小bar，不會被破壞。 */
  padding: 2rem;
  min-height: 10vh;
  align-items: center;
  /* nav bar 可以跟著視窗改變位置，不會擠在一起。 */
  flex-wrap: wrap;
}

/* CHILDREN */
nav ul {
  display: flex;
  flex: 1 1 40rem;
  justify-content: space-around;
  align-items: center;
  list-style: none;
}

#logo {
  flex: 2 1 40rem;
  font-family: "Pattaya", sans-serif;
  font-weight: 400;
}

```

### Hero Section

1. 對圖片進行設置，上面疊一層陰影`linear-gradient`，增加字的可視度。

```css=
#hero{
    background: linear-gradient(rgba(0, 0, 0, 0.6), transparent),
      url("img/landing-page.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
}
```
2. `min-height: 90vh;`圖片的最小高度，讓圖片伸展開來。

```css=
#hero {
  /* 讓圖片伸展開來 */
  min-height: 90vh;
  /* img setting */
  background: linear-gradient(rgba(0, 0, 0, 0.8), transparent),
    url("img/landing-page.jpg");
  /* 對圖片進行設置 */
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  /* h2，h3 */
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* 讓字向中央對齊 */
  text-align: center;
}

```

讓h3跟旁邊撐開距離

![](https://i.imgur.com/jnlu2ue.jpg)

```css=
#hero h3 {
  padding: 5rem;
}
```

更改button的樣式

```css=
button {
  padding: 2rem 6rem;
  background-color: #4c6e97;
  border: none;
  color: white;
  font-size: 1.8rem;
  cursor: pointer;
}

button:hover {
  background-color: #27394e;
}

```

更改字體

> HTML

```html=
<link
  href="https://fonts.googleapis.com/css2?family=Pattaya&family=Poppins:wght@400;500&display=swap"
  rel="stylesheet"
/>
```

> CSS

```css=
body {
  font-family: "Poppins", sans-serif;
}
```

更改特定的字體粗細度

`font-weight: normal`，更改它weight。

```css=
h3 {
  font-size: 3rem;
  font-weight: normal;
}
```

### Media Query

> 可以確認他什麼size的時候，body會不見。

```css=
/* 小於932px的時候會消失 */
@media screen and (max-width: 932px) {
  html {
    display:none
  }
}
```

更改字體大小，還有header的padding。


```css=
@media screen and (max-width: 932px) {
  html {
    font-size: 45%;
  }
  nav {
    text-align: center;
  }
  #logo {
    padding: 1rem;
  }
}
```

## Creating the City Section

[Browser Prefixes](https://autoprefixer.github.io/)

[Can I Use](https://caniuse.com/)

[Easing](https://easings.net/)

[Hex to RGB](https://www.rgbtohex.net/hextorgb/)

![](https://i.imgur.com/goqF6rq.png)

### City Section HTML

```html=
<section id="locations">
  <header class="locations-head">
    <h2>The Perfect Travelling Experience.</h2>
    <h3>
      we cover everything from picking the perfect hotel,<br />flight and
      Travelly destination.
    </h3>
    <img src="img/cloud.png" class="moving-cloud-1 cloud" alt="" />
    <img src="img/cloud.png" class="moving-cloud-2 cloud" alt="" />
  </header>
</section>
```

### City Section CSS 解析

1. `overflow: hidden;`，不讓cloud跑出去，加在根元素section上。
2. `text-decoration: underline;`，不一定每個瀏覽器都支援。
3. `text-decoration-thickness: 0.5rem`，加粗底線。 

![](https://i.imgur.com/gPYtlJO.png)

4. 在字上面加上顏色，chrome需要在前面加上-webkit私有前綴才可以使用。

![](https://i.imgur.com/KsLdsWK.png)

```css=
.locations-head h3 {
    padding: 4rem 0rem;
    /* 只呈現在h3上的漸層 */
    background: linear-gradient(#131c27, #663b34);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}
```

### City Section All CSS
  
```css=
/* Locations Section */

#locations {
    min-height: 100vh;
    background: linear-gradient(rgba(0, 0, 0, 0.5), transparent),
        url("img/new-york-page.png");
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    position: relative;
    overflow: hidden;
}

.locations-head {
    width: 90%;
    margin: auto;
}

.locations-head h2 {
    padding: 1rem 0rem;
    text-decoration: underline;
    text-decoration-thickness: 0.5rem;
}

.locations-head h3 {
    padding: 4rem 0rem;
    /* 只呈現在h3上的漸層 */
    background: linear-gradient(#131c27, #663b34);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
}

.cloud {
    position: absolute;
    right: 0;
    top: 0;
}
```
### Cloud Animation

1. transform，位移。
    `translate(mx,my)`，元素以參考點為中心，X軸位移mx距離，Y軸位移my距離。
2. animation屬性，normal，reverse，alternate，reverse-alternate。
 [參考網站](https://www.runoob.com/cssref/css3-pr-animation-direction.html)
3. `infinite`為重複播放。
4. `@keyframe`製作動畫。
```css=
.cloud {
  position: absolute;
  /* 固定在右上角 */
  right: 0;
  top: 0;
}

.moving-cloud-1 {
  animation: cloudAnimation 3s infinite alternate ease-in-out;
}

.moving-cloud-2 {
  top: 20%;
  /* 讓他在原始的雲後面 */
  z-index: -1;
  opacity: 0.5;
  /* 添加動畫 */
  /* infinite讓她自己循環 */
  /*  forward不循環  */
  animation: cloudAnimation 3.5s infinite alternate ease-in-out;
}


/* 動畫 */
/* 0%，50%，100% */
@keyframes cloudAnimation {
  from {
    transform: translate(10%, -10%);
  }
  to {
    transform: translate(0%, 0%);
  }
}
```

### Media Query

5. `-webkit-text-fill-color: white;`，讓字體變白色。
6.  `background: rgb(19, 28, 39, 0.6)`，加上一層背景。

![](https://i.imgur.com/f5YOZ75.png)


```css=
/* Media Query */
@media screen and (max-width: 932px) {
    html {
        font-size: 45%;
    }

    nav {
        text-align: center;
    }

    #logo {
        padding: 2rem;
    }

    .cloud {
        height: 40rem;
        /* 避免觸發選取 */
        pointer-events: none;
    }

    .moving-cloud-1 {
        z-index: -1;
    }

    .moving-cloud-2 {
        z-index: -2;
    }

    .locations-head h2 {
        text-align: center;
    }

    .locations-head h3 {
        background: rgb(19, 28, 39, 0.6);
        -webkit-text-fill-color: white;
    }
}

```

## Card Section

![](https://i.imgur.com/cyN8ni6.png)


### Card HTML
```pug=
section#benefits
  header.benefits-head
    h2 The Perfect Travel
    h3
      | We cover everything for picking the perfect hotel
      br
      | to flight and
      |             destination.
  .cards
    .card
      .card-icon
        img(src='icons/route-solid.svg' alt='')
      h4 Travel
      p Travel in over 250 countries with no effort.
    .card
      .card-icon
        img(src='icons/bed-solid.svg' alt='')
      h4 Hotel
      p Hotel located near popular areas.
    .card
      .card-icon
        img(src='icons/plane-departure-solid.svg' alt='')
      h4 Fly
      p Flight included in every purchased trip.

```
### Benefits Section Css

![](https://i.imgur.com/WiUjbuq.png)

```css=
.benefits-head {
  background: #343c44;
  padding: 3rem;
  min-height: 30vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
  text-align: center;
}

.benefits-head h3 {
  padding: 1rem;
}
```
![](https://i.imgur.com/jih7ZX3.png)


1. 卡片`min-height: 70vh;`，flex預設會有stretch，所以他會延伸到頁面下(70vh)，只要加上`align-item:center`就可以使他致中縮短。
2. `box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.5)`，box-shadow: x y blur 顏色
3. 開始調整前先把img改成`height:100px`，較為美觀。
```css=
.cards {
  width: 90%;
  margin: auto;
  /*  在根元素加上display:flex就可以使他平行  */    
  display: flex;
  min-height: 70vh;
  /* flex預設會有strech所以他會延伸到頁面下(70vh)，
   * 只要加上align-item:center就可以使他縮短。 */
  align-items: center;
  /*  responsive  */
  flex-wrap: wrap;
}
.card {
  /* 也可以讓圖片致中 */
  text-align: center;
  flex: 1 1 25rem;
  /*  每一張圖片都有40vh的高度  */
  min-height: 40vh;
  margin: 2rem 5rem;
  /*  陰影:x y blur 顏色  */
  box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.5), 0px 20px 20px rgba(0, 0, 0, 0.1);
}
.cards img {
  /* 開始調整前先把img改成100px，較為美觀。 */
  /* height: 100px; */
  /*  調整圖片(路徑，飛機)大小  */
  max-width: 15%;
  margin: 2rem;
}

.card h4,
.card p {
  padding: 1rem;
  line-height: 2;
}

.card-icon {
  background: #27394e;
}

```

## Form Section 

![](https://i.imgur.com/IidPbxy.jpg)


### Form HTML

注意表格的html怎麼寫!

```pug=
scection#contact
  .form-wrapper
    header.form-head
      h2 Contact Us
    form(action='https://formspree.io/f/mnqoggek' method='POST')
      .name-form
        label(for='name') Name:
        input#name(type='text' name='name' required='')
      .email-form
        label(for='email') Email:
        input#email(type='email' name='email' required='')
      button(value='Send' type='submit') Submit

```

### Form Css
1. `width: 100%`，延伸整個button。
2. `border-bottom-left-radius: 20px`，改變button特定的邊邊圓角。
  
```css=
/* 圖片 */
#contact {
  min-height: 100vh;
  background: linear-gradient(rgba(0, 0, 0, 0.5), transparent),
    url("img/contact-mountain.png");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Form後面的背景色 */
.form-wrapper {
  background: rgba(19, 28, 39, 0.8);
  width: 60%;
  color: white;
  border-radius: 20px;
}

.form-head {
  text-align: center;
  padding: 4rem;
}

.name-form,
.email-form {
  padding: 3rem;
  text-align: center;
}

.form-wrapper label {
  /* 框框與字體的距離 */
  margin: 0rem 3rem;
}

.form-wrapper button {
  /* 讓他延伸整個button */
  width: 100%;
  padding: 2rem;
  margin-top: 8rem;
  /*  讓他變成圓角  */
  border-bottom-left-radius: 20px;
  border-bottom-right-radius: 20px;
}

 /* 讓輸入框框變大 */
.form-wrapper input {
  padding: 1rem 3rem;
}
```

![](https://i.imgur.com/QJROdNm.png)

## Footer

![](https://i.imgur.com/hhN3kEo.png)

### Footer HTML

`&copy;`，Travelly旁邊的小c。

```pug=
footer
  .footer-wrapper
    h5 Travelly &copy;
    ul
      li
        a(href='#' title='twitter-social-media')
          img(src='icons/twitter.svg' alt='twitter-social-media')
      li
        a(href='#' title='youtube-social-media')
          img(src='icons/youtube.svg' alt='youtube-social-media')
      li
        a(href='#' title='instagram-social-media')
          img(src='icons/instagram.svg' alt='instagram-social-media')

```

### Footer Css

1. flex不是在所有地方都會定位，要在有可以排列的(ul)的地方才可以做使用，如果放在footer裡面就無法排列。

```css=
footer {
  color: white;
  background-color: rgb(19, 28, 39, 1);
}

.footer-wrapper {
/* 要在有ul的地方才可以做使用，如果放在footer裡面就無法排列。 */
  display: flex;
  padding: 2rem;
  width: 90%;
  margin: auto;
  align-items: center;
  min-height: 10vh;
  flex-wrap: wrap;
}

footer h5 {
  flex: 1 1 40rem;
}
footer ul {
  display: flex;
  list-style: none;
  flex: 1 1 40rem;
  justify-content: space-between;
  align-items: center;
}

/* Keyboard */
button:focus {
  background: #2e435c;
  outline-style: solid;
}

```

### Media Query

1. `.form-wrapper {width: 100%;}`，讓input框框不會突出背景色。

2. `pointer-events: none;`，不會點到雲。

```css=
/* Media Query */
@media screen and (max-width: 932px) {
  html {
    font-size: 45%;
  }
  nav {
    text-align: center;
  }
  #logo {
    padding: 1rem;
  }
  .cloud {
    height: 40rem;
    pointer-events: none;
  }
  .moving-cloud-1 {
    z-index: -1;
  }
  .moving-cloud-2 {
    z-index: -2;
  }
  .locations-head h3 {
    background: rgb(19, 28, 39, 0.8);
    -webkit-text-fill-color: white;
  }
  /* 讓input不會突出背景色 */
  .form-wrapper {
    width: 100%;
  }
  /* 字體致中 */
  footer {
    text-align: center;
  }
  footer h5 {
    padding-bottom: 3rem;
  }
}

```

### Submitting Forms(Bonus)

[formspree](https://formspree.io/)

接受信件回覆的一種方法。

```htmlembedded=
<form action="https://formspree.io/f/mnqoggek" method="POST">
   <div class="name-form">
      <label for="name">Name:</label>
      <input id="name" type="text" name="name" required />
   </div>
   <div class="email-form">
      <label for="email">Email:</label>
      <input
         id="email"
         type="email"
         name="email"
         required
         name="_replyto"
         />
   </div>
   <button value="Send" type="submit">Submit</button>
</form>
```