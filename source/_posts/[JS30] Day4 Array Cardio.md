---
title: '[JS30] Day4 - Array Cardio'
author: Phoebe
tags: Javascript
categories: JS 30
date: 2021-05-24 11:07:11
---

## 學習到的知識點

- `filter()` 篩選資料
- `map()` 與 `forEach()` 的差異
- `sort()` 的穩定排序
- `reduce()` 的用法
- `querSelectorAll()` 篩選資料
- `sort()` 與 `spilt()` 組合技

<!--more-->

## 思考分析

JS30 的 Day4 為使用八個範例，介紹關於 `Array` 的各種操作。

作者 wes bos 已經設定好資料們。

![](https://i.imgur.com/Sn6zLlG.png)

### 1. `filter()`

第一個練習為，篩選出生年為 1500 - 1600 的 inventor。

`filter` 的用法就是給了一組資料給它，它會從這組資料保留符合條件，做為一個新的陣列。

```javascript=
// 1. Filter the list of inventors for those who were born in the 1500's
let ans = inventors.filter(function(inventor){
  return inventor.year >= 1500 && inventor.year < 1600;
})
```

也可以使用箭頭函式的寫法，使用箭頭函式就不需要加上`return`。

**補充箭頭函式與一般函數的差異**

```javascript=
let ans = inventors.filter(inventors => inventor.year >= 1500 && inventor.year < 1600);
```

結果：

這裡有個小技巧，使用 `console.table` 就可以用表格看資料，相較之下比較好閱讀。

![](https://i.imgur.com/wcFFErh.png)

### 2. `map()`

第二題的練習為，將 inventors 內的 `first` 與 `last` 組合成一個陣列。

這裡會和`forEach`一起做比較。

#### `map`

```javascript=
let ans = inventors.map(inventor => inventor.first + ' ' + inventor.last)
console.table(ans);
```

`map` 會自動 `return` 新的陣列。

#### `ForEach`

```javascript=
let ans = [];
inventors.forEach(inventor => ans.push(inventor.first + ' ' + inventor.last))
console.table(ans);
```

`foreach` 不會回傳陣列，所以需要自己設一個陣列，再將資料推進去。

假設，今天要對陣列做一件事情，沒有要產生新的內容，就要使用 `forEach`。

如果希望是產生一個對應的**新陣列**，這時候就可以用`map`。

最大的差別就是，有沒有產生一個新的陣列。

結果：
![](https://i.imgur.com/ou1GOFr.png)

### 3. `sort()`

第三題為依據生日，由大至小排序所有的 inventor。

`sort` 會有穩定排序和非穩定排序。

當數值一樣時，將會維持原本的排序，就是穩定排序。

使用數值相減的方法會相對穩定，會分成三類，<0，==0，>0。

寫法一：

```javascript=
const ordered = inventors.sort(function(a, b) {
    if(a.year > b.year) {
        return 1;
    } else {
        return -1;
    }
});
```

寫法二：

```javascript=
let ans = inventors.sort((a,b)=> a.year - b.year);
console.table(ans);
```

結果：

預設由小排到大。
![](https://i.imgur.com/EhbGvHI.png)

### 4. `reduce()`

第四題為，加總所有 inventor 在世的時間。

第一次 `total` 等於 0 ( 預設值 )，`total` 從 0 開始 ( 最後面的 `0` 所代表的意思)，經過每一次的 inventor 資料。

`reduce` 會回傳值 ( 總和 )。

```javascript=
// 第一次示意
1 => total = 0.inventor => { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 }
// 第二次示意
2 => total = 76,inventor => { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 }
```

寫法一：

```javascript=
let total = inventors.reduce((total,inventor)=>{
  return total + inventor.passed - inventor.year
},0)
```

也可以使用 `forEach` 完成。

寫法二：

```javascript=
let total = 0;
inventors.forEach((inventor)=>{
  total += inventor.passed - inventor.year
})
console.log(total);
```

### 5. `sort()`

第五題為，依據年齡由大至小排序所有的 inventor 。

```javascript=
let ans = inventors.sort((a,b)=>{
return (a.passed - a.year) - (b.passed - b.year)
})

console.table(ans);
```

![](https://i.imgur.com/iMLp9SY.png)

### 6. `querySelectorAll`

第六題為，列出 [這頁維基百科](https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris) 所有包含 "de" 的名字，透過 `querySelectorAll` 選取資料。

寫法一：

```javascript=
let ary = []
document.querySelectorAll('.mw-category-group li a').forEach((a)=>{
    ary.push(a.title)
})

let ans = ary.filter(title=>title.indexOf('de') !== -1)
```

![](https://i.imgur.com/OvVh95i.png)

寫法二：

`Array.from`可以將 `NodeList` 轉換成為 `Array`，才能對其進行 `map` 操作 ( `map` 是`Array` 的方法， `NodeList` 沒有)。

加上 `filter`，`includes` 做文字的篩選，若存在 "de" 就回傳 true 加入陣列。

```javascript=
const category = document.querySelector('.mw-category');
const links = Array.from(category.querySelectorAll('a'));
const de = links
            .map(link => link.textContent)
            .filter(streetName => streetName.includes('de'));
```

### 7. `sort()` & `split()`

第七題為，依照 `lastName` 排序所有 people 的資料。

```javascript=
let ans = people.sort((a,b)=>{
  let [aFirst,aLast] = a.split(', ');
  let [bFirst,bLast] = b.split(', ');
  return aLast > bLast ? 1 : bLast > aLast ? -1 : 0;
})
console.table(ans);
```

結果：
這邊 Ambrose 會出現在 Aneurin 前面，是因為他判斷到了第二個字。
![](https://i.imgur.com/MwubbXB.png)

三元運算子的解釋：

```javascript=
if(aLast > bLast){
    1
}else if(bLast > aLast){
    -1
}else{
    0
}
```

若想指判斷第一個字，就加上 `[0]`，按照原始的排序去排列 (穩定排序) 。

```javascript=
let ans = people.sort((a,b)=>{
let [aFirst,aLast] = a.split(', ');
let [bFirst,bLast] = b.split(', ');
  return aLast[0] > bLast[0] ? 1 : bLast[0] > aLast[0] ? -1 : 0;
})
console.table(ans);
```

![](https://i.imgur.com/EQFhMSg.png)

### 8. `reduce()`

第八題為，分別計算 data 內每個種類的數量。

寫法一：

```javascript=
let ans = data.reduce((obj,content)=>{
  if(!obj[content]) obj[content] = 1
  else obj[content] += 1

  return obj
},{})

console.table(ans);
```

寫法二：

```javascript=
const transportation = data.reduce(function (obj, item) {
    if (!obj[item]) {
        obj[item] = 0;
    }
    obj[item]++;
        return obj;
}, {});
```

## 延伸學習

## 參考網站

[Array.prototype.map() - JavaScript | MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

[「JS30 紀錄＆心得」04 - Array Cardio Day 1 | Gua's Note](https://guahsu.io/2017/05/JavaScript30-04-Array-Cardio-Day-1/)
