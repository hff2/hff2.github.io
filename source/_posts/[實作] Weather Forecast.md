---
title: "[實作] Weather Forecast"
author: Phoebe
tags: Javascript
categories: Portfolio
date: 2021-02-08 11:07:11
---

## 學習到的知識點

### CSS

- Media Query
- 偽元素
- `transform`
- `box-shadow`
<!--more-->

### JS

- ajax

## 簡介

[Demo](https://)

可以選擇區域查看當天與未來七天的天氣。

![](https://i.imgur.com/y2btZmS.jpg)

## HTML

### 結構

```html=
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Weahter Forecast</title>
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css"
      integrity="sha512-HK5fgLBL+xu6dm/Ii3z4xhlSUyZgTT9tuc/hSrtw6uzJOvgRr2a9jyxxT1ely+B+xFAmJKVSTbpM/CuL7qxO8w=="
      crossorigin="anonymous"
    />
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div class="container">
      <div class="areaSelect">
        <select id="areaSelect">
          <option value="0">淡水區</option>
          <option value="1">鶯歌區</option>
        </select>
      </div>
      <div class="header">
        <h1>請選擇一區域查看天氣</h1>
      </div>
      <div id="new_area">
      </div>
    </div>
    <script
      src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.js"
      integrity="sha512-WNLxfP/8cVYL9sj8Jnp6et0BkubLP31jhTG9vhL/F5uEZmg5wEzKoXp1kJslzPQWwPT1eyMiSxlKCgzHLOTOTQ=="
      crossorigin="anonymous"
    ></script>
    <script src="app.js"></script>
  </body>
</html>

```

### 超連結

選單使用到[fontawesome](https://fontawesome.com/)的 icon，需插入連結才可以使用。

```html=
<link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css"
      integrity="sha512-HK5fgLBL+xu6dm/Ii3z4xhlSUyZgTT9tuc/hSrtw6uzJOvgRr2a9jyxxT1ely+B+xFAmJKVSTbpM/CuL7qxO8w=="
      crossorigin="anonymous"
/>
```

## CSS

[完整 Code](https://github.com/hff2/My-Projects/blob/weather-forecast/Weather_Forecast/style.css)

### Media Query

`min-width`為最小為 1300px，所以當網頁寬度**大於**1300px 時，就套用下方的 style。

反之，如果小於 1300px，則照舊。

`min-width`和`max-width`在寫得時候有點搞混，以此紀錄。

```css=
@media screen and (min-width: 1300px) {
  img {
    height: 15rem;
    width: 15rem;
    margin: 3rem;
  }
  .eachInfo h1 {
    font-size: 4rem;
  }
  .eachInfo h3 {
    font-size: 2.3rem;
  }
  .header h1 {
    font-size: 5rem;
  }
}

```

### 選單樣式

瀏覽器預設的選單樣式不太好看，因為在這邊改了預設的選單樣式。

#### 去除私有前綴

```css=
appearance: none;
-moz-appearance: none;
-webkit-appearance: none;
```

#### 偽元素加上 icon

`\f358`為 icon 的編號，`Font Awesome 5 Free`為使用 fontawesome icon 需要加上的。

```css=
{
  content: "\f358";
  font-family: "Font Awesome 5 Free";
}
```

固定圖案後面的背景

```css=
{
  top: 0;
  right: 0;
  width: 5rem;
  height: 5rem;
}
```

將圖案放到中間

```css=
{
  text-align: center;
}
```

滑鼠放到 icon 上的動畫，`transition`為動畫進行的時間，`:hover`為偽類(要放在偽元素前面)。

```css=
.areaSelect:before {
  transition: 0.3s;
}

.areaSelect:hover:before {
  background: #ebebeb;
}
```

```css=
.areaSelect select {
  border-radius: 2rem;
  background-color: #ebebeb;
  color: black;
  padding: 1rem;
  width: 20rem;
  height: 5rem;
  border: none;
  font-size: 2rem;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  appearance: none;
  -moz-appearance: none;
  -webkit-appearance: none;
  outline: none; /*  點擊後產生的邊框  */
}

.areaSelect:before {
  content: "\f358";
  font-family: "Font Awesome 5 Free";
  position: absolute;
  top: 0;
  right: 0;
  width: 5rem;
  height: 5rem;
  text-align: center;
  border-top-right-radius: 1.7rem;
  border-bottom-right-radius: 1.7rem;
  line-height: 5rem;
  color: #353535;
  font-size: 2.8rem;
  background: #bbbbbb;
  transition: 0.3s;
  pointer-events: none;
}

.areaSelect:hover:before {
  background: #ebebeb;
}

```

### 漂浮動畫

#### 陰影效果

`box-shadow: h-shadow v-shadow blur spread color inset`

`h-shadow`：水平位移距離
`v-shadow`：垂直位移距離
`blur`：模糊半徑
`spread`：擴散距離
`color`：顏色
`inset`：內陰影

`transform`有許多種用法，可以到[MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/transform)參考。

`translate`就是位移的改變。

```css=
.now_weather {
  background-color: rgb(214, 214, 214);
  border: 2px solid rgb(170, 170, 170);
  border-radius: 25px;
  width: 20rem;
  margin: auto;
  border-radius: 25px;
  /*  運用到box-shadow和transition  */
  box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.3);
  transition: 0.4s;
  margin-bottom: 1.3rem;
}

.now_weather:hover {
  background-color: rgb(255, 255, 255);
  /*  hover之後，改變陰影和位移，就可以做出漂浮效果  */
  box-shadow: 5px 5px 60px rgba(0, 0, 0, 0.3);
  transform: translate(-5px, -5px);
}
```

## JS

### 取得 API

到[中央氣象局開放資料平臺之資料擷取 API](https://opendata.cwb.gov.tw/dist/opendata-swagger.html)網站註冊後，取得 API。

```javascript=
const api = `https://opendata.cwb.gov.tw/api/v1/rest/datastore/F-D0047-071?Authorization=CWB-9374D590-DA77-47DF-B677-81B70B7016E6`;
$.ajax({
  url: api,
  method: "GET",
  dataType: "json",
  success: function (res) {
    console.log(res);
    data = res.records.locations[0];
  },
});
```

1. 註冊完成後，點選 try it out，然後輸入 Authorization。

![](https://i.imgur.com/CoeHaqm.png)

2. 因為下面還有許多欄位，一開始不知道還要輸入什麼，然後就在網路上看了其他人的文章也沒有人特別提及。所以，我就直接按下最下面的 Execute，讓他產生連結，過程大約需要一分鐘。

![](https://i.imgur.com/D0EjUgQ.png)

3. 產生 Request URL 後就可以直接複製使用

![](https://i.imgur.com/4ASfX1b.png)

使用 Jquery 的 ajax 方法，就可以看到回傳的資料。

![](https://i.imgur.com/lUbJdwb.png)

### 取得和更換區域名稱

將得到的資料放到`areaName`變數裡，`areaIndex`為選單選擇到的區域的 Index，使用`change`只要有變動就會觸發事件。

再將內容更換到`.header`上。

```javascript=
function selectArea(data, areaIndex) {
  let area = data.location;
  let areaName = area[areaIndex].locationName;
  $(".header").html(`<h1>${areaName}</h1>`);
}

areaSelect.addEventListener("change", (e) => {
  areaIndex = e.target.value;
  selectArea(data, areaIndex);
});
```

### 取得天氣資料

取出資料的步驟比較繁雜，一個區域會獲得 15 筆天氣資料，再輸入需要的資料編號，就可以取出資料，放到變數裡。

`data.location[areaIndex].weatherElement[1].time[0].elementValue[0].value`

就可以取出平均溫度。

![](https://i.imgur.com/0E2lg1h.png)

#### 遇到的問題

未來七天的天氣使用`for迴圈`取資料時，`for (let i = 3; i < 14; i += 2)`，i 最後是`i+=2`，不是`i+2`，需要特別注意，因為原本寫成`i+2`，導致程式當掉。

` $("#future_weather").append(``)`，因為未來七天的資料有七筆，如果使用`.html()`就會只顯示最後一筆，所以需要改成` .append(``) `

```javascript=
function showWeatherInfo(data, areaIndex) {
  area = data.location;
  // 平均溫度
  let areaTemp =
    area[areaIndex].weatherElement[1].time[0].elementValue[0].value;
  // 天氣描述
  let areaDesc =
    area[areaIndex].weatherElement[6].time[0].elementValue[0].value;
  // 最高體感溫度
  let areaTempH =
    area[areaIndex].weatherElement[5].time[0].elementValue[0].value;
  // 最低體感溫度
  let areaTempL =
    area[areaIndex].weatherElement[11].time[0].elementValue[0].value;
  // 呼叫判斷Icon函式
  let areaIcon = setIcon(areaDesc);
  // 得到的資料放到html裡，在最後產生一個future_div放一周的天氣
  $("#new_area").html(`
  <div class="now_weather">
  <div class="showIcons">${areaIcon}</div>
    <h2>現在天氣</h2>
    <h3>${areaDesc}</h3>
    <p>均溫: ${areaTemp} °C</p>
    <p class="temp">${areaTempL}°C / ${areaTempH}°C</p>
  </div>
    <div id="future_weather"></div>
    `);

  // 取得為來七天的天氣
  for (let i = 3; i < 14; i += 2) {
    // 分別是資料的3,5,7,9,11,13
    let timeIndex = i;
    // 取得日期
    let FutureTime =
      area[areaIndex].weatherElement[1].time[timeIndex].startTime;
    let FutureTimeSubstr = FutureTime.substr(5, 5);
    // 平均溫度
    let FutureTemp =
      area[areaIndex].weatherElement[1].time[timeIndex].elementValue[0].value;
    // 天氣描述
    let FutureDesc =
      area[areaIndex].weatherElement[6].time[timeIndex].elementValue[0].value;
    // 最高體感溫度
    let FutureTempH =
      area[areaIndex].weatherElement[5].time[timeIndex].elementValue[0].value;
    // 最低體感溫度
    let FutureTempL =
      area[areaIndex].weatherElement[11].time[timeIndex].elementValue[0].value;
    // 呼叫判斷Icon函式
    let icon = setIcon(FutureDesc);
    // 利用new_area產生的div future_weather
    // 使用append將資料全部輸出到HTML上
    $("#future_weather").append(`
    <div class="eachInfo">
      <h1>${FutureTimeSubstr}</h1>
      <div class="showIcons">${icon}</div>
      <h3>${FutureDesc}</h3>
      <p>均溫: ${FutureTemp} °C</p>
      <p>${FutureTempL}°C / ${FutureTempH}°C</p>
    </div>
  `);
  }
}

areaSelect.addEventListener("change", (e) => {
  areaIndex = e.target.value;
  showWeatherInfo(data, areaIndex);
  selectArea(data, areaIndex);
});
```

### 加上 icon

這邊很簡單的就是進行判斷，然後再將天氣的描述放到函式。但是我在這邊卡了很久。

#### 遇到的問題

1. 原本想使用[skyicons](https://darkskyapp.github.io/skycons/) api，最後也成功出現，但是遇到一種狀況，比如說，如果希望晴時多雲的圖案出現，需要被觸發兩次才會出現，過程中也一直無法排解問題，嘗試了許久只好換成圖片的方式。

![](https://i.imgur.com/IKjtXMG.png)

2. 原本使用直接在函式裡判斷好 Info 之後直接顯示在 HTML，但是發現這樣未來七天的天氣又需要使用迴圈，整個函數會變得很龐大，最後以呼叫函數然後傳入 Info，判斷完成後，再`return`結果。

```javascript=
function setIcon(WeatherInfo) {
  if (WeatherInfo == "晴時多雲" || WeatherInfo == "多雲時晴") {
    return "<img src='img/cloudy.svg'>";
  } else if (
    WeatherInfo == "多雲短暫雨" ||
    WeatherInfo == "陰時多雲短暫雨" ||
    WeatherInfo == "陰短暫雨" ||
    WeatherInfo == "多雲短暫陣雨" ||
    WeatherInfo == "陰短暫陣雨"
  ) {
    return "<img src='img/rainy.svg'>";
  } else if (
    WeatherInfo == "多雲時陰" ||
    WeatherInfo == "多雲" ||
    WeatherInfo == "陰時多雲" ||
    WeatherInfo == "多雲時陰短暫雨" ||
    WeatherInfo == "多雲時陰短暫陣雨" ||
    WeatherInfo == "陰天" ||
    WeatherInfo == "陰時多雲短暫陣雨"
  ) {
    return "<img src='img/cloud.svg'>";
  } else if (
    WeatherInfo == "多雲短暫陣雨或雷雨" ||
    WeatherInfo == "陰短暫陣雨或雷雨" ||
    WeatherInfo == "陰時多雲短暫陣雨或雷雨" ||
    WeatherInfo == "多雲時陰短暫陣雨或雷雨"
  ) {
    return "<img src='img/thunder.svg'>";
  }
}
```

### 後紀

天氣 API 不會很難完成，但我也是研究了三天才做到還可以的程度，完成後才發覺沒有想像中困難。

一開始不知道該如何存取資料就一些時間查資料，後來遇到 for 迴圈的問題，一直不知道為什麼執行程式時就會直接當掉，後來才發現是少寫=。

使用 html 資料只出現一筆時，花了一些時間才找到 bug。

skyicons api 的圖案也嘗試了很久，但最後還是無法，因為他本來是給一個叫做 darksky 的 api 資料做使用，所以最後只好折衷使用 img 代替。

## 參考文章

[一般天氣預報-今明 36 小時天氣預報](https://opendata.cwb.gov.tw/dataset/forecast/F-C0032-001)

[中央氣象局開放資料平臺之資料擷取 API](https://opendata.cwb.gov.tw/dist/opendata-swagger.html)

[CSS3 box-shadow 區塊陰影](https://abgne.tw/css/css3-lab/css3-box-shadow.html)
