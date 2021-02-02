---
title: HTML5 Drag and Drop API 筆記
author: Phoebe
date: 2021-02-02 10:46:36
tags: Javascript
categories: Javascript
---
## 簡述
HTML5 中的 Drag & Drop API 可以讓我們在瀏覽器中做到**拖曳元素**、**排序元素**、或者是讓使用者透過拖拉的方式把要上傳的檔案拉到瀏覽器當中。
<!--more-->
在學習 HTML5 Drag & Drop API 時，最重要的是去區分 Drag Source 和 Drop Target，因為它們會需要各自去監聽不同的事件。

![](https://i.imgur.com/8YizrxC.png)


- `Drag Source` 指的是**被點擊要拖曳的物件，也就是藍色的圓**，通常是一個 element。
- `Drop Target` 指的是**拖曳的物件被放置的區域，也就是右邊的綠色區域**，通常是一個 div container。

## Drag & Drop 主要事件

Drag & Drop 提供的事件主要包含`dragstart, drag, dragend, dragenter, dragover, dragleave, drop`，其中有些是針對 Drag Source 的，有些則是針對 Drop Target 的，整理如下表：


| x | Drag Source | Drag Target | 解釋 |
| ------ | -------- | -------- | ----|
|1| dragstart     |      | **開始**拖曳元素時觸發此事件 (點擊元素的瞬間) |
|2| drag     |  dragenter    | **拖曳**元素時觸發此事件 |
|3|      |   dragover   | 當元素拖曳到**有效位置**放置則觸發此事件 |
|4|      |   dragleave   | 拖曳的元素**離開有效的位置**時觸發|
|5|      |   drop   | 在**有效位置**上**放置**元素時觸發此事件 (放下元素) |
|6|  dropend |      | 當拖曳**結束**時會觸發此事件 |

- drag：在 drag source **被拖曳**時會持續被觸發。
- dragover：當拖曳的 drag source 到 drop target 上方時會持續被觸發。

**記得要針對被拖曳的物件取消預設行為（default）**




## 參考連結

[製作可拖曳的元素（HTML5 Drag and Drop API）](https://pjchender.blogspot.com/2017/08/html5-drag-and-drop-api.html)

[详解Html5关于拖拽（Drag 和 drop）的使用和事件](https://blog.csdn.net/weixin_41229588/article/details/106574573?ops_request_misc=&request_id=&biz_id=102&utm_term=dragleave&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-5-106574573.pc_search_result_before_js)