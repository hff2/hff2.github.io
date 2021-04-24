---
title: keydown, keypress, keyup的差異
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-04-23 09:20:02
---

# 鍵盤的操作

網頁中鍵盤的操作分為三種，`keydown`，`keypress`，`keyup`。

可以在此[網站](http://keycode.info/)查詢鍵值。

<!--more-->

## 比較它們的差異

### keydown

keydown 就是指按下的那瞬間，任何的鍵盤按下都可以取的對應的按鍵鍵碼。a -> 65，s -> 83。

### keypress

與 keydown 不同在於，keypress 只會針對可以輸出文字符號的按鍵有效，ESC、方向鍵...等。這類沒有辦法輸出文字的鍵，是無法觸發事件。

### keyup

而 keyup 是指放開鍵盤的那個剎那，觸發該事件。取得 keyCode 的部分基本上跟 keydown 是一樣。

三者事件的觸發優先順序為：keydown → keypress → keyup

## 參考文章

[比較 keydown, keypress, keyup 的差異. 在網頁的鍵盤事件操作有三種 keydown, keypress… | by Tommy | Medium](https://medium.com/@yitailin/%E6%AF%94%E8%BC%83-keydown-keypress-keyup-%E7%9A%84%E5%B7%AE%E7%95%B0-4e873ba17e81)
