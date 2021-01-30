---
title: Grid 排版練習
author: Phoebe
date: 2020-12-22 11:32:46
tags: HTML&CSS
categories: Web
---
[參考網站](https://css-tricks.com/snippets/css/complete-guide-grid/)

## 簡介
Grid號稱是Css最強大的排版系統。
屬於二維空間(2-dimensional)，所以能夠同時更改column跟row。

flex屬於一維空間，一次只能更改一個。

<!--more-->

## 實作

### 1 flex:grid

[Grid-demo-01](https://codepen.io/phoebe-ho/pen/ZEpBJNb?editors=1100)

將grid放到容器裡，使內容都以gird方式排列。

在沒有做任何更改時，呈現的樣子為橫排。

![](https://i.imgur.com/di62MOl.png)

---

### 2 grid-template-columns

[Grid-demo-01](https://codepen.io/phoebe-ho/pen/ZEpBJNb?editors=1100)

column為直的，所以一格一格切開。

1fr為填滿剩下的空格。

```css=
.boxes{
  display: grid;
  grid-template-columns: 10rem 1fr 10rem;
}
```

![](https://i.imgur.com/GDLYWrC.png)

---

### 3 grid-template-columns:repeat(次數,空間)

[Grid-demo-02](https://codepen.io/phoebe-ho/pen/gOwLGOB)

repeat(次數，空間)的用法，使用repeat就不用一個一個輸入。


```css=
.boxes{
    border: 1rem solid rgb(117, 117, 117);
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;

}
```

```css=
.boxes{
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}
```

```css=
.boxes{
  border: 1rem solid rgb(117, 117, 117);
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```
```css=
.boxes{
    border: 1rem solid rgb(117, 117, 117);
  display: grid;
  grid-template-columns: 10% repeat(2, 10fr) 10%;
}
```

![](https://i.imgur.com/DpCqE7G.png)

![](https://i.imgur.com/fc88KeU.png)

---

### 4 grid-template-rows

[Grid-demo-02](https://codepen.io/phoebe-ho/pen/gOwLGOB)

row橫向排版，auto為自動排版，在容器有使用padding時，會自動撐開距離。

```css=
.boxes{
    border: 1rem solid rgb(117, 117, 117);
  display: grid;
  grid-template-columns:  repeat(3, 1fr);
  grid-template-rows:  20rem  20rem 20rem;
}
```


![](https://i.imgur.com/AYIQ0xe.png)

![](https://i.imgur.com/CWqeyUX.png)

---

### 5 grid-template-areas


[Grid-demo-03](https://codepen.io/phoebe-ho/pen/vYXyeyz)

自己創造出順序，再開個area依序放入，要留下的空格用.代替。


>自己命名的部分
```css=
.box1 {
  background-color: rgb(188, 216, 233);
  grid-area: box1;
}
.box2 {
  background-color: rgb(211, 166, 166);
    grid-area: box2;
}

.box3 {
  background-color: rgb(163, 126, 160);
    grid-area: box3;
}

.box4 {
  background-color: rgb(139, 163, 132);
    grid-area: box4;
}

.box5 {
  background-color: rgb(177, 176, 146);
    grid-area: box5;
}
```
> 創造順序
```css=
.boxes {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-areas: "box2 box1 box3"
                       "box4 . box5";
}
```

![](https://i.imgur.com/4kxR3U2.png)

> 使用定位的方式填滿空間




```css=
.boxes-2 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-areas: "box2 box2 box3"
                       "box4 box1 box5";
}

.boxes-3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-areas: "box2 box2 box3"
                       "box4 box1 box3"
                       "box5 box5 box5";
}
```

![](https://i.imgur.com/Y8WYPHg.png)

---

### 6 Grid-column，Grid-row

[Grid-demo-04](https://codepen.io/phoebe-ho/pen/PoGbJeM)

grid-column順序為：起頭不為0，1為最左邊，2為往右數一格，直向數過去。
grid-row同上，橫向數過去。

```css=
.box1 {
  background-color: rgb(188, 216, 233);
  grid-column:1/2;
  }
.box2 {
  background-color: rgb(211, 166, 166);
    grid-column:2/3;
    }

.box3 {
  background-color: rgb(163, 126, 160);
  grid-column:3/4;
  grid-row:1/3;
 }

.box4 {
  background-color: rgb(139, 163, 132);
}

.box5 {
  background-color: rgb(177, 176, 146);
}
```

![](https://i.imgur.com/aZpu4b0.png)

---

### 7 grid-column-gap，grid-row-gap，grid-gap

[Grid-demo-04](https://codepen.io/phoebe-ho/pen/PoGbJeM)

在物件中留空隙的方法。

```css=
.boxes-2{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-column-gap: 1rem;
}
.boxes-3{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-row-gap: 1rem;
}

.boxes-4{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}
```

![](https://i.imgur.com/y5W1JnT.png)

---

### 8 justify-items: center，align-items: center

[Grid-demo-04](https://codepen.io/phoebe-ho/pen/PoGbJeM)

將物件置中。

Grid裡的置中，不是flex-start，而是只有start，end。

```css=
.boxes-5{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
  justify-items: center;  /*  end，start  */
  align-items: center;
}
```

![](https://i.imgur.com/IyLN9QZ.png)

---

### 9 grid-template-rows

[Grid-demo-04](https://codepen.io/phoebe-ho/pen/PoGbJeM)

上下留20rem的距離。

```css=
.boxes-6{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 20rem  20rem;
  grid-gap: 1rem;
  justify-items: center;  /*  end，start  */
  align-items: center;
}
```

![](https://i.imgur.com/VIcYIVH.png)


---

### 10 justify-self

[Grid-demo-04](https://codepen.io/phoebe-ho/pen/PoGbJeM)

選取單元素做偏移。

```htmlembedded=
    <div class="boxes boxes-7">
      <div class="box1 box">
        <h1>Box1</h1>
      </div>
      <div class="box2 box">
        <h1>Box2</h1>
      </div>
      <div class="box3 box">
        <h1>Box3</h1>
      </div>
      <div class="box4 box">
        <h1>Box4</h1>
      </div>
      <div class="box5 box">
        <h1>Box5</h1>
      </div>
    </div>
```

```css=
.boxes-7{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 20rem  20rem;
  grid-gap: 1rem;
  justify-items: center;  /*  end，start  */
  align-items: center;
}
.boxes-7 .box2{
  justify-self: end;
  align-self:start;
}
.boxes-7 .box5{
  justify-self: start;
  align-self:center;
}
```


![](https://i.imgur.com/kqYE9Q1.png)
