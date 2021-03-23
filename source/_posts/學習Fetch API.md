---
title: 學習 Fetch API
author: Phoebe
tags: Javascript
categories: Javascript
date: 2021-03-23 15:12:59
---

## 認識 XHR

XMLHttpRequest（XHR）是 Javascript 較古老的 API，取得伺服器資料，卻不需要頁面重整(reload)。

<!--more-->

非同步的網路架構稱為 AJAX，但現在已經不推薦使用，因為其結構設計已經無法應對現今複雜的 Web 環境，且容易掉入 Callback Hell 裡。

```html=
function reqOnload () {
  const data = JSON.parse(this.responseText);
  console.log(data)
}

function reqError (err) {
  console.log('錯誤', err)
}

// 宣告一個 XHR 的物件
var Req = new XMLHttpRequest();
// 定義連線方式
Req.open('get', 'https://randomuser.me/api/', true);
// 送出請求
Req.send();
// 如果成功就執行 reqOnload()
Req.onload = reqOnload;
// 失敗就 reqError()
Req.onerror = reqError;
```

可以看的出來請求資料的過程偏向複雜。

XHR 製作時，每次都要新建(`new`)一個請求的實體。

而 AJAX 的網站，通常也不會只做一次請求。為了讓程式碼更容易維護及開發，大多開發者都會使用**框架**來包裝這類行為。

## jQuery 請求框架

jQuery 的請求框架十分容易閱讀與使用，只需要將網址帶進去，就可以得到`response`。

```javascript=
$.ajax({
    type: "method",
    url: "url",
    data: "data",
    dataType: "dataType",
    success: function (response) {

    }
});
```

## Fetch

### 基本用法

Fetch 在使用時與 jQuery 的`$.ajax`十分相近。

不同的地方在於:

- 使用 ES6 的`Promise`做回應
- `then` 做為下一步
- `catch` 作為錯誤回應

```javascript=
fetch('網址')
.then(function(response) {
    // 處理 response
}).catch(function(err) {
    // 錯誤處理
});
```

### Fetch 的 Request 屬性

| 屬性     | 設定值                                                     |
| -------- | ---------------------------------------------------------- |
| url      | 第一個參數，一定要填的項目，代表需要 fetch 對象的網址      |
| method   | GET、POST、PUT、DELETE、HEAD ( 預設 GET )                  |
| headers  | 要求相關的 Headers 物件 ( 預設 {} )                        |
| mode     | cors、no-cors、same-origin、navigate ( 預設 cors )         |
| referrer | no-referrer、client 或某個網址 ( 預設 client )             |
| body     | 要加到要求中的內容 ( 如果 method 為 GET 或 HEAD 則不設定 ) |

### Fetch 的 Response 屬性

| 屬性       | 設定值                                 |
| :--------- | :------------------------------------- |
| headers    | 包含與 response 相關的 Headers 物件    |
| ok         | 成功回傳 true，不成功回傳 false        |
| status     | 狀態代碼，成功為 200                   |
| statusText | 狀態文字，成功為 ok                    |
| type       | response 的類型，例如 basic、cors...等 |
| url        | response 的 url                        |

### Fetch 的 Response 方法

| 方法          | 設定值                                                                    |
| ------------- | ------------------------------------------------------------------------- |
| json()        | 返回 Promise，resolves 是 JSON 物件                                       |
| text()        | 返回 Promise，resolves 是 text string                                     |
| blob()        | 返回 Promise，resolves 是 blob ( 非結構化物件資料，例如文字或二進位資料 ) |
| arrayBuffer() | 返回 Promise，resolves 是 ArrayBuffer ( 有多少 bytes )                    |
| clone()       | 建立 Response 的複製物件                                                  |
| error()       | 返回 Response 的錯誤物件                                                  |

### Fetch 的 Get 用法

```javascript=
const url = `https://reqres.in/api/users`;

fetch(url, {method:'GET'})
    .then(result => {
        console.log(result);
});
```

![](https://i.imgur.com/easlXiM.png)

### Fetch 的 Post 用法

在使用 POST 方法時，需要有`headers`與`JSON.stringify`來轉換成 string 方式傳遞

```javascript=
fetch("https://reqres.in/api/users/",{
    method:'POST',
    // tell fetch you going to send json
    headers:{
        'Content-Type':'application/json'
    },
    // 轉換格式
    body:JSON.stringify({
        name:"Phoebe"
    })
})  .then(res=>{
    return res.json();
}).then(data => console.log(data))
```

data 的內容會被寫入伺服器。

![](https://i.imgur.com/fZulLhO.png)

## 參考文章

[JavaScript Fetch API 使用教學 - OXXO.STUDIO](https://www.oxxostudio.tw/articles/201908/js-fetch.html)

[鐵人賽：ES6 原生 Fetch 遠端資料方法 | 卡斯伯 Blog - 前端，沒有極限](https://wcc723.github.io/javascript/2017/12/28/javascript-fetch/)

[Beginners Guide To Fetching Data With (AJAX, Fetch API & Async/Await) - DEV Community](https://dev.to/bjhaid_93/beginners-guide-to-fetching-data-with-ajax-fetch-api--asyncawait-3m1l)

[Learn Fetch API In 6 Minutes](https://www.youtube.com/watch?v=cuEtnrL9-H0)
