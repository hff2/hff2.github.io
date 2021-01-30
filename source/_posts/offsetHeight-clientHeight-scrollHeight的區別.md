---
title: offsetHeight, clientHeight, scrollHeight的區別?
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-01-26 20:08:13
---
## 寬度/高度

> 計算寬度或高度之前，要先理解，border和捲軸的寬度/高度需要被包含在內嗎？

| 編號 | 寬度 | 高度 |
| - | ------------- | ------------- |
| 1 | clientWidth | clientHeight |
| 2 | offsetWidth | offsetHeight |
| 3 | scrollWidth | scrollHeight |

<!--more-->

1. `clientWidth`/`clientHeight` 是元素所包含的「子元素」的寬度/高度，其中包含了`padding`，但不包含`border`及捲軸。

![](https://i.imgur.com/1WsvK43.png)

2. `offsetWidth`/`offsetHeight` 是「元素本身」的寬度/高度，並完整了包含了`border`、捲軸及`padding`，`但不包含margin`。

![](https://i.imgur.com/bHXpCQt.png)

3. `scrollWidth`/`scrollHeight` 也是元素所包含的「子元素」的「完整」寬度和高度，其中包含了超出捲軸之外的部分的寬度與高度。

![](https://i.imgur.com/oQ3l6ov.png)

## 相對位置

| 編號 | 左方       | 上方      |
|:----:| ---------- | --------- |
|  1   | clientLeft | clientTop |
|  2   | offsetLeft | offsetTop |
|  3   | scrollLeft | scrollTop |



1. `clientLeft`/`clientTop`，元素本身內外的水平/垂直距離，也就是左邊/上面的邊界寬度。
![](https://i.imgur.com/wDpao44.png)

2. `offsetLeft`/`offsetTop`，元素本身相對於母元素的水平/垂直距離。

![](https://i.imgur.com/dKJzTfL.png)

3. `scrollLeft`/`scrollTop`，是「內容」被捲動的距離，也就是內容頂端和捲軸頂端的相對距離。

![](https://i.imgur.com/tsJq40x.png)

## 常見應用

前端經常實作的一個功能就是無限捲動，當捲軸捲到接近底部的時候，會向API要更多資料。

所以，我們必須知道「內容底端距離捲軸底端的距離」，下方咖啡色框框的部分。

雖然我們已經知道「內容頂端與捲軸頂端的距離」是`.scrollTop`，但很遺憾的是並沒有`.scrollBottom`這個屬性，

但是，我們可以知道「內容底端距離捲軸底端的距離」＝ `elem.scrollHeight` - `elem.scrollTop` - `elem.clientHeight`。

以圖來說，內容底端距離捲軸底端的距離就是，咖啡色 = 綠色 - 黃色 - 紫色。

完整內容高度 (scrollHeight) = 內容頂端與捲軸頂端的距離 (scrollTop) + 捲軸本身高度 (clientHeight) + 內容底端與捲軸底端的距離。

![](https://i.imgur.com/xKhVBNo.png)

## 參考文章

[一次搞懂 clientHeight/clientWidth/offSetHeight/offsetWidth/scrollHeight/scrollWidth/scrollTop/scrollLeft 的區別](https://shubo.io/element-size-scrolling/)

[圖片來源](https://javascript.info/size-and-scroll)