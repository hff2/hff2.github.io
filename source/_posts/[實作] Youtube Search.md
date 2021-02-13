---
title: '[實作] Youtube Search'
author: Phoebe
tags: Javascript
categories: Portfolio
date: 2021-02-12 11:07:11
---

## 功能

利用Youtube API，可以搜尋Youtube影片。

有查看上一頁和下一頁的功能，點擊標題連結可以在該頁撥放影片。
<!--more-->
## 學習到的知識點

### CSS
- .clearfix

### JS
- `$.get`
- `$.each`
- `fancy box`

## 簡介
[Demo](https://hff2.github.io/My-Projects/Youtube_Search/index.html)

## HTML
### 結構
```html=
<body>
    <div class="container">
      <header>
        <h1>Search<span> Videos</span></h1>
        <p>Search all Youtube videos</p>
      </header>
      <section>
        <form
          id="search-form"
          class="search-form"
          name="search-form"
          onsubmit="return search()"
        >
        <!-- 需注意這邊的按下enter時，會return function  -->
          <div class="fieldcontainer">
            <input
              type="search"
              id="query"
              class="search-field"
              placeholder="Search Youtube..."
            />
            <input type="submit" name="search-btn" id="search-btn" value="" />
          </div>
        </form>
        <ul id="results"></ul>
        <div id="buttons"></div>
      </section>
      <footer>
        <p>Copyright &copy; 2021, All Right Reserved</p>
      </footer>
    </div>
    <script src="./js/script.js"></script>
    <script src="./js/jquery.fancybox.pack.js"></script>
    <script>
      $(document).ready(function () {
        $(".fancybox").fancybox();
      });
    </script>
  </body>
```

## CSS

[完整Css Code](https://github.com/hff2/My-Projects/blob/youtube-search/Youtube_Search/css/style.css)

### clearFix

在使用 float 的時候經常會遇到圖片超出預設的寬度，但只要使用clearfix，就可以使圖片和容器寬度一樣。

```css=
.clearfix {
  clear: both;
}
```
### box-shadow

發現了一個網站可以直接複製做好的shadow做使用。

[Beautiful CSS box-shadow examples](https://getcssscan.com/css-box-shadow-examples)

## JS
### Search Bar animation

這邊使用Chaining鏈式，做了searchBar的動畫，在JS裡控制 css的 animation。

做出一種當滑鼠點擊輸入框時，會產生伸縮的效果。

![](https://i.imgur.com/s1RZAlf.png)

![](https://i.imgur.com/2v0V5uN.png)


```javascript=
//Searchbar Handler
$(document).ready(function () {
  var searchField = $("#query");
  var icon = $("#search-btn");

  //Focus Handler
  $(searchField).on("click", function () {
    $(this).animate(
      {
        width: "100%",
      },
      500
    );
    $(icon).animate(
      {
        right: "10px",
      },
      500
    );
  });
  // Blur Event Handler
  $(searchField).on("blur", function () {
    if (searchField.val() == "") {
      $(searchField).animate(
        {
          width: "45%",
        },
        500
      );
      $(icon).animate(
        {
          right: "360px",
        },
        500
      );
    }
  });

  $("#search-form").submit(function (e) {
    e.preventDefault();
  });
});
```
### 取得Youtube API資料

利用網址可以取得的json資料。

![](https://i.imgur.com/UD3uRzQ.png)


取得的資料

![](https://i.imgur.com/fO5TCK5.png)


#### $.get功能

- `part`: 這個參數是為了避免大家呼叫 API 時得到太多**不相關的資訊**，所以用 part 來定義要取得的資料範圍。在 Search 的情況下，設定為 `part:snippet` 。
- `type`：限制搜尋結果為 video、channel 或 playlist
- `q`：搜尋關鍵字
- `key`: 金鑰

```javascript=
function search() {
  // Clear Result
  $("#result").html("");
  $("#buttons").html("");

  // Get Form Inupt
  q = $("#query").val();

  $.get(
    "https://www.googleapis.com/youtube/v3/search",
    {
      part: "snippet,id",
      q: q,
      type: "video",
      key: "AIzaSyDUQUDfpg_6iA_ycnD5yaAYLSPc495aa",
    },
    // 取得data裡的Token方便之後使用
    function (data) {
      var nextPageToken = data.nextPageToken;
      var prevPageToken = data.prevPageToken;

      // Log Data
      console.log(data);
    }
  );
}
```


### search函式，使用each讀取每一筆資料


目標為取得items的每一筆item，使用`each`方法。

![](https://i.imgur.com/1Jocnbc.png)

```javascript=
$.each(data.items, function (i, item) {
// Get Ouput
var output = getOutput(item);

// Display Result
$("#results").append(output);
});

var buttons = getButtons(prevPageToken, nextPageToken);

// Display Buttons
$("#buttons").append(buttons);
```


### getOutput函式

過濾資料，取得需要的部分，建立成output字串。

在這邊就可以得到影片與內容的資訊，然後更改video的樣式。

![](https://i.imgur.com/xt3b5Iu.png)

![](https://i.imgur.com/fqSZ3vx.png)



```javascript=
// Build Output
function getOutput(item) {
  // 過濾資料
  var videoId = item.id.videoId;
  var title = item.snippet.title;
  var description = item.snippet.description;
  var thumb = item.snippet.thumbnails.high.url;
  var channelTitle = item.snippet.channelTitle;
  var videoDate = item.snippet.publishedAt;

  // Build Output String
  // 建立output字串
  var output =
    "<li>" +
    '<div class="list-left">' +
    '<img src="' +
    thumb +
    '">' +
    "</div>" +
    '<div class="list-right">' +
    "<h3>" +
    title +
    "</h3>" +
    '<small>By <span class="cTitle">' +
    channelTitle +
    "</span> on " +
    videoDate +
    "</small>" +
    "<p>" +
    description +
    "</p>" +
    "</div>" +
    "</li>" +
    '<div class="clearfix"></div>' +
    "";
  // 一般function最後都需要return
  return output;
}

```

### 產生下一頁與上一頁的Button

在`search()`函式裡，有取得`nextPageToken`和`prevPageToken`的數值，所以在`getButtons()`函式可以直接調用。

![](https://i.imgur.com/1qLJ4c3.png)

![](https://i.imgur.com/4OMbg5B.png)


```javascript=
var buttons = getButtons(prevPageToken, nextPageToken);

// Build the buttons
function getButtons(prevPageToken, nextPageToken) {
// 如果是沒有prevPageToken，就只需要顯示next page button
  if (!prevPageToken) {
    var btnoutput =
      '<div class="button-container">' +
      '<button id="next-button" class="paging-button" data-token="' +
      nextPageToken +
      '" data-query="' +
      q +
      '"' +
      'onclick="nextPage();">Next Page</button></div>';
  } else {
// 有prevPageToken 才會產生兩個Button
    var btnoutput =
      '<div class="button-container">' +
      '<button id="prev-button" class="paging-button" data-token="' +
      prevPageToken +
      '" data-query="' +
      q +
      '"' +
      'onclick="prevPage();">Prev Page</button>' +
      '<button id="next-button" class="paging-button" data-token="' +
      nextPageToken +
      '" data-query="' +
      q +
      '"' +
      'onclick="nextPage();">Next Page</button></div>';
  }

  return btnoutput;
}
```

有nextPageToken就會有兩個Button

![](https://i.imgur.com/7Zb7kRp.png)

![](https://i.imgur.com/qQFzPgk.png)


### nextPage函數使 next Button可以使用

```javascript=
// Next Page Function
function nextPage() {
  var token = $("#next-button").data("token");
  var q = $("#next-button").data("query");

  // Clear Results
  $("#results").html("");
  $("#buttons").html("");

  // Get Form Input
  q = $("#query").val();

  // Run GET Request on API
  // 再做一次讀取資料
  $.get(
    "https://www.googleapis.com/youtube/v3/search",
    {
      part: "snippet, id",
      q: q,
      pageToken: token,
      type: "video",
      key: "AIzaSyDUQUDfpg_6iA_ycnD5yaAYLSPc495aa",
    },
    function (data) {
      var nextPageToken = data.nextPageToken;
      var prevPageToken = data.prevPageToken;

      // Log Data
      console.log(data);

      $.each(data.items, function (i, item) {
        // Get Output
        var output = getOutput(item);

        // Display Results
        // 將讀取到的資料append到html
        $("#results").append(output);
      });

      var buttons = getButtons(prevPageToken, nextPageToken);

      // Display Buttons
      $("#buttons").append(buttons);
    }
  );
}
```

### prevPage函數使prev Button可以使用

功能和nextButton一樣，改變一些變數。

```javascript=
// Prev Page Function
function prevPage() {
  var token = $("#prev-button").data("token");
  var q = $("#prev-button").data("query");

  // Clear Results
  $("#results").html("");
  $("#buttons").html("");

  // Get Form Input
  q = $("#query").val();

  // Run GET Request on API
  $.get(
    "https://www.googleapis.com/youtube/v3/search",
    {
      part: "snippet, id",
      q: q,
      pageToken: token,
      type: "video",
      key: "AIzaSyDUQUDfpg_6iA_ycnD5yaAYLSPc495aa",
    },
    function (data) {
      var nextPageToken = data.nextPageToken;
      var prevPageToken = data.prevPageToken;

      // Log Data
      console.log(data);

      $.each(data.items, function (i, item) {
        // Get Output
        var output = getOutput(item);

        // Display Results
        $("#results").append(output);
      });

      var buttons = getButtons(prevPageToken, nextPageToken);

      // Display Buttons
      $("#buttons").append(buttons);
    }
  );
}
```

### fancy box 


到[fancy box](http://fancybox.net/) 官網下載檔案，然後放到Project裡。

![](https://i.imgur.com/kY7hjVW.png)

最後再更改一些地方就可以使用

引入這個版本的jquery，fancybox 才可以正常運行，筆者原先使用3.5.1版本就無法運行，會直接開一個新的頁面，並不是我們要的效果。

> HTML

```html=
<!-- 1.11.1版本 -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>

<!-- 引入檔案 -->
<script src="./js/jquery.fancybox.pack.js"></script>
<link rel="stylesheet" href="./css/jquery.fancybox.css" />
```

```javascript=
<script>
  $(document).ready(function () {
    $(".fancybox").fancybox();
  });
</script>
```

> JS

js的部分需要加上超連結，就可以在fnacybox打開影片。

因為css放在css資料夾裡，所以需要開啟`jquery.fancybox.css`去更改圖片的路徑才可以使用(叉號與圖片與Loading圖)。

```html=
'<h3><a class="fancybox fancybox.iframe" href="http://www.youtube.com/embed/' +
videoId +
'">' +
title +
"</a></h3>" +
```

![](https://i.imgur.com/500c0Zw.jpg)

## 後記

Youtube API和天氣API比起來，有許多很技巧性的方法像是each還有fancy box，目前尚未完全學會，之後會做細分成更多更小的筆記一一學習。


## 參考文章

[vsc-initialized是什么](https://www.jianshu.com/p/70b7589fefd1)

[JQuery Chaining](https://ithelp.ithome.com.tw/articles/10090569)

[.clearfix](https://zh-tw.learnlayout.com/clearfix.html) 