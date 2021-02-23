---
title: CSS 私有前綴
author: Phoebe
tags: HTML&CSS
categories: Web
date: 2021-02-23 00:56:50
---

`-webkit-appearance` 為使用系統預設的外觀。

`-webkit-appearance: none`，去除瀏覽器的預設樣式。

webkit是一種瀏覽器的私有前綴，是瀏覽器對新css實現的一個提前支持。

-webkit是指，webkit內核的瀏覽器(Safari和Google)，moz是Firefox內核的瀏覽器。

> 為什麼會出現webkit跟moz這種私有前綴?

因為制定HTML和CSS標準的組織W3C動作較慢。

通常，W3C組織成員提出新屬性，比如說`border-radius`，但要審核一個屬性通過需要很多審查，瀏覽器商不想等這麼久，就會在瀏覽器中先加入支持。

但是，避免W3C公布標準時有變更，就會加入一個私有前綴，比如`-webkit-border-radius`，通過這種方式來提前支持屬性。