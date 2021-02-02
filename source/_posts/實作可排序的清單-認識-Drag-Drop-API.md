---
title: '實作可排序的清單 認識 Drag & Drop API '
author: Phoebe
tags: Javascript
categories: Portfolio
date: 2021-02-01 01:31:08
---
## 功能

- 創建有序列表
- 隨機產生列表
- 使用者可以隨意拖曳項目到不同位置
- 檢查按鈕檢查順序是否正確
- 錯誤顯示紅色，正確顯示綠色

<!--more-->
## 學習到的知識點

### HTML

- `draggable="true"`
- `data-*` attribute

### JS

- Drag and Drop API
- `.setAttribute()`
- `[...]`
- `.sort()`
- `map()`

## 簡介

[Demo](https://)

![](https://i.imgur.com/xcWI6qP.png)


## HTML

### 結構

![](https://i.imgur.com/tuy9I0r.png)

```html=
<body>
    <h1>TOP 10 World's Most Valuable Brands in 2021</h1>
    <p>Drag and drop the items into their corresponding spots</p>
    <!--  JS動態產生ul  -->
    <ul class="draggable-list" id="draggable-list"></ul>
    <button class="check-btn" id="check">
      Check Order
      <i class="fas fa-paper-plane"></i>
    </button>
</body>
```

## CSS

[完整Code](https://github.com/hff2/My-Projects/blob/sortable-list/Sortable_List/style.css)

### `flex`:`flex-grow flex-shrink flex-basic`

`flex:` 放大比例 縮小比例 計算元素是否有多餘空間，預設值為auto。

`flex:1`的意思為`flex: 1 1 0`，所以數字與`<i class="fas fa-grip-lines"></i>`的空間，最小最大都會是1，所以不會變形。

```css=
.draggable-list li {
  background-color: #fff;
  display: flex;
  flex: 1;
}
```
```css=
.draggable {
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px;
  flex: 1;
}
```

## JS

[完整Code](https://github.com/hff2/My-Projects/blob/sortable-list/Sortable_List/script.js)

### 宣告變數

排序的內容為，[2021世界十大最有價值的品牌](https://fxssi.com/top-10-most-valuable-brands)。

##### 原生JS

```javascript=
const draggable_list = document.getElementById("draggable-list");
const check = document.getElementById("check");

const powerfulBrands = [
  "Apple Inc.",
  "Amazon.com Inc.",
  "Microsoft",
  "Google",
  "Samsung",
  "Coca-Cola",
  "Toyota",
  "Mercedes-Benz",
  "McDonald’s",
  "Disney",
];

// Store listitems
const listItems = [];

let dragStartIndex;
```

##### Jquery

```javascript=
const draggable_list = $('#draggable-list')[0]
const powerfulBrands = [
  "Apple Inc.",
  "Amazon.com Inc.",
  "Microsoft",
  "Google",
  "Samsung",
  "Coca-Cola",
  "Toyota",
  "Mercedes-Benz",
  "McDonald’s",
  "Disney",
];

const listItems = [];

let dragStartIndex;
```

### 將陣列放入DOM裡

#### 展開運算子

在 ES6 中，新增了一個 `[ … ]` 的關鍵字，這個關鍵字在不同時間點，有不同的效果，有些時候它會被當作展開運算子(spread operator)使用，有時候則是被當作其餘運算子（rest operator）使用。

展開運算子，是**把許多的參數轉換成一個陣列**，而展開運算子則是可以**把陣列中的元素取出**。

在[實作電影定位介面](https://hff2.github.io/2021/01/17/%E5%AF%A6%E4%BD%9C-%E9%9B%BB%E5%BD%B1%E9%99%A2%E8%A8%82%E4%BD%8D%E4%BB%8B%E9%9D%A2/)時，也有使用到此技巧。

#### `.setAttribute()`

`Element.setAttribute(name, value)`

增加**指定名稱**和**值**的新屬性，或者把一個現有的屬性設定為指定的值。

舉例來說

[setAttribute Demo](https://codepen.io/phoebe-ho/pen/qBqELJX)

1. 用html設定一個Button
```html=
<body>
  <button>Hello World</button>
</body>
```
2. setting設定字為紅色
```css=
.setting {
  color: red;
}
```
3. `b`變數取得`button`，再利用`setAttribute`增加**樣式**與**方法屬性**。

```javascript=
var b = document.querySelector("button");

b.setAttribute("id", "helloButton");
b.setAttribute("class", "setting");
b.setAttribute("onclick", "javascript:alert('test!')");
console.log(b)
```

![](https://i.imgur.com/RvocDck.png)


#### HTML5 中的 `data-*` attribute 屬性

在製作網頁的過程中，我們常常會添加一些**自己需要用到的屬性名稱**，以方便自己容易理解，為了要**避免**大家在 HTML 結構中隨意的添加屬性，在 HTML5 中就多了 `data-*` attribte 這個屬性，其中的 `*` 就是一個可以**自定義**的名稱。例如：`data-key='83'` 或者是 `data-item='1'`。

而這邊的範例就是`data-index`。


##### 原生JS

```javascript=
createList();

// Insert list items into DOM
function createList() {
  [...powerfulBrands].forEach((company, index) => {
    // listItem為空的陣列，放入powerfulBrands的陣列。
    const listItem = document.createElement("li");

    listItem.setAttribute("data-index", index);

    listItem.innerHTML = `
        <span class="number">${index + 1}</span>
        <div class="draggable" draggable="true">
          <p class="person-name">${company}</p>
          <i class="fas fa-grip-lines"></i>
        </div>
      `;

    listItems.push(listItem);

    draggable_list.appendChild(listItem);
  });
}
```

>顯示出來的樣子

![](https://i.imgur.com/2Pgp68p.png)

##### Jquery

```javascript=
.forEach((company, index) => {
      const listItem = document.createElement("li");

      listItem.setAttribute("data-index", index);

      listItem.innerHTML = `
        <span class="number">${index + 1}</span>
        <div class="draggable" draggable="true">
          <p class="company-name">${company}</p>
          <i class="fas fa-grip-lines"></i>
        </div>
      `;

      listItems.push(listItem);

      draggable_list.appendChild(listItem);
    });
  addEventListeners();
}

```
### 隨機排列item順序

這邊使用的方法是

1. 先產生隨機數
2. 再利用`sort()`方法由小排到大
3. 完成每次都能產生隨機排列的順序
 

當只有`.map((a) => ({ value: a, sort: Math.random() }))`時，person會印出`map()`賦予的sort，可以注意到都是random( 0 - 1之間 )的值。

![](https://i.imgur.com/G4bLHe3.png)


`.map()`每個都取得隨機變數後，利用`sort()`由小排到大。

![](https://i.imgur.com/Mpge5Uq.png)

排列完大小後，用`map()`取出值就好。

![](https://i.imgur.com/bjkG8Fn.png)


#### `sort()`用法解釋

[Array.prototype.sort()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

```javascript=
const numbers = [1, 3, 110, 40, 302];
console.log(
  numbers.sort(function (a, b) {
    return a - b;
  })
);
```
![](https://i.imgur.com/EnHw7Mw.png)


##### 原生JS
 
```javascript=
[...powerfulBrands]
   // array有sort方法，所以利用random產生sort值
  .map((a) => ({ value: a, sort: Math.random() }))
  // 產生了之後，sort方法比大小，這樣每次重整後的順序都會不同
  .sort((a, b) => a.sort - b.sort)
  // 只取得value
  .map((a) => a.value)
  .forEach((person, index) => {
      console.log(person)
```

##### Jquery

```javascript=
[...powerfulBrands]
.map(function (data) {
  return {
    value: data,
    sort: Math.random(),
  };
})
.sort(function (a, b) {
  return a.sort - b.sort;
})
.map(function (data) {
  return data.value;
})
```

### 設定事件監聽Function

[HTML5 Drag and Drop API 筆記](https://hff2.github.io/2021/02/02/HTML5-Drag-and-Drop-API-%E7%AD%86%E8%A8%98)

針對能夠被拖曳的元素，在其 HTML 標籤上添加屬性 `draggable="true"`

以下整理成表格，方便之後判斷。這次實作沒有運用到`dropend`。

| x | Drag Source | Drag Target | 解釋 |
| ------ | -------- | -------- | ----|
|1| dragstart     |      | **開始**拖曳元素時觸發此事件() |
|2| drag     |  dragenter    | **拖曳**元素時觸發此事件 |
|3|      |   dragover   | 當元素拖曳到**有效位置**放置則觸發此事件 |
|4|      |   dragleave   | 拖曳的元素**離開有效的位置**時觸發|
|5|      |   drop   | 在**有效位置**上**放置**元素時觸發此事件 |
|6|  dropend |      | 當拖曳**結束**時會觸發此事件 |

##### Javascript

```javascript=
function addEventListeners() {
  const draggables = document.querySelectorAll(".draggable");
  const dragListItems = document.querySelectorAll(".draggable-list li");

  draggables.forEach((draggable) => {
    draggable.addEventListener("dragstart", dragStart);
  });

  dragListItems.forEach((item) => {
    item.addEventListener("dragover", dragOver);
    item.addEventListener("drop", dragDrop);
    item.addEventListener("dragenter", dragEnter);
    item.addEventListener("dragleave", dragLeave);
  });
}

check.addEventListener("click", checkOrder);

```

##### Jquery

Jquery沒有相關的寫法，只有在 jqueryUI裡面才有。所以，以下都只有原生JS的寫法。



#### `dragEnter()`，`dragLeave()`

- `dragenter`，拖曳元素時觸發的事件。
- `dragleave`，拖曳的元素離開有效的位置時觸發。

這邊做出的效果是，當拖曳的元素到其他元素上時，會變色。拖曳第一欄到第二欄上時，第二欄就變色。

![](https://i.imgur.com/3xuG1Nw.png)

但是當拖曳欄位不在有效範圍時，第二欄的欄位就不會變色。

![](https://i.imgur.com/K1lHAyi.png)

##### 原生JS
```javascript=
function dragEnter() {
  // console.log('Event: ', 'dragenter');
  this.classList.add("over");
}

function dragLeave() {
  // console.log('Event: ', 'dragleave');
  this.classList.remove("over");
}
```


#### `dragStart()`，`dragDrop()`

.closet是一個遍歷的方法。

[.closetDemo](https://codepen.io/phoebe-ho/pen/poNvYBq) 

`.getAttribute`就是前面提到的，增加指定名稱和值的新屬性，所以可以得到index。

- `dragstart`，**開始拖曳**元素時觸發此事件。
- `drop`，在**有效位置**上放置元素時，觸發此事件。

當開始拖曳元素欄位時，就開始記錄Index，停止拖曳元素時，也記錄當下的Index。

再利用`swapItems()`，交換內容。

##### 原生JS

```javascript=
function dragStart() {
  // console.log('Event: ', 'dragstart');
  dragStartIndex = +this.closest("li").getAttribute("data-index");
  console.log(dragStartIndex)
}

function dragDrop() {
  // console.log('Event: ', 'drop');
  const dragEndIndex = +this.getAttribute("data-index");
  swapItems(dragStartIndex, dragEndIndex);
  this.classList.remove("over");
}
```
當我移動第一個時，dragStartIndex的改變，就會跳出0...以此類推。

![](https://i.imgur.com/iGcVK52.png)


#### `dragOver()`

避免預設行為，才使用`swapItems()`避免被觸發提交。
- `dragOver`，當元素拖曳到有效位置放置則觸發此事件。

在dragOver函式裡加上避免預設行為的`preventDefault()`，避免被不停觸發。

##### 原生JS

```javascript=
function dragOver(e) {
  // console.log('Event: ', 'dragover');
  e.preventDefault();
}
```

#### `SwapItems()`

交換items，使用到`appendChild`方法。

##### 原生JS

```javascript=
//Swap list items that are drag and drop
function swapItems(fromIndex, toIndex) {
  const itemOne = listItems[fromIndex].querySelector(".draggable");
  const itemTwo = listItems[toIndex].querySelector(".draggable");

  // console.log(itemOne, itemTwo);
  listItems[fromIndex].appendChild(itemTwo);
  listItems[toIndex].appendChild(itemOne);
}
```


### 檢查順序是否正確

- `trim()`將字串去除空白

##### 原生JS
```javascript=
// Check the order of list items
function checkOrder() {
  listItems.forEach((listItem, index) => {
    const randomBrands = listItem.querySelector(".draggable").innerText.trim();

    if (randomBrands !== powerfulBrands[index]) {
      listItem.classList.add("wrong");
    } else {
      listItem.classList.remove("wrong");
      listItem.classList.add("right");
    }
  });
}

check.addEventListener("click", checkOrder);
```


## 參考文章

[JavaScript中setAttribute用法介紹](https://codertw.com/%E5%89%8D%E7%AB%AF%E9%96%8B%E7%99%BC/289731/)

[什麼是 HTML 5 中的資料屬性（data-* attribute）](https://pjchender.blogspot.com/2017/01/html-5-data-attribute.html)

[製作可拖曳的元素（HTML5 Drag and Drop API）](https://pjchender.blogspot.com/2017/08/html5-drag-and-drop-api.html)


[Node Element 在 appendChild 後消失（disappear）!?](https://pjchender.blogspot.com/2017/06/js-node-element-appenchild-disappear.html)
