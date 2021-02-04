---
title: '[實作] Github Finder'
author: Phoebe
date: 2021-02-04 14:43:58
tags: Javascript
categories: Portfolio
---
## 功能

搜索Github用戶，並顯示個人訊息和最新的Repository。

## 學習到的知識點

### JS
- Ajax 實作串接 Github API
- Jquery Ajax

<!--more-->
## 簡介
[Demo](https://hff2.github.io/My-Projects/Github_Finder/index.html)

![](https://i.imgur.com/2l4aMZ1.png)


## HTML
### 結構

HTML內容不多，多為用JS動態產生的內容。

```html=
<body>
<nav class="navbar navbar-dark bg-primary mb-3">
  <div class="container">
    <a href="#" class="navbar-brand">GitHub Finder</a>
  </div>
</nav>
<div class="container searchContainer">
  <div class="search card card-body">
    <h1>Search GitHub Users</h1>
    <p class="lead">Enter a username to fetch a user profile and repos</p>
    <div id="error"></div>
    <input
      type="text"
      id="searchUser"
      class="form-control"
      placeholder="GitHub Username..."
    />
  </div>
  <br />
  <div id="profile"></div>
</div>
<footer class="mt-5 p-3 text-center bg-light">GitHub Finder &copy;</footer>
<script src="script.js"></script>
</body>
```

## CSS

使用[Bootswatch](https://bootswatch.com/)

## JS
### 取得資料，過濾資料

- 過濾取到api裡面的資料，這邊使用`change`，使用`keyup`時，會不停的觸發搜尋，所以輸入完成後按下enter才會執行。

- url裡面放的資料可以透過網址先觀察，只要更改後面的名字，就可以取到不同人的資料。

![](https://i.imgur.com/x14KVGK.png)




- data裡面放的資料為`clent_id`，`client_secret`，在還沒有放置時，一開始都可以正常存取，但後來會出現403拒絕存取的錯誤，在[stackoverflow](https://stackoverflow.com/questions/39907742/github-api-is-responding-with-a-403-when-using-requests-request-function)找到解答，需要有**valid User-Agent header**，所以要加上`clent_id`，`client_secret`。

- `success`為成功運行後執行的function，`insertProfile()`函式利用物件的方法，將json檔取出，這邊先過濾一整包資料，因為會出現no data的狀況。相較之下，repository就不會出現沒有資料顯示null的狀況，所以只要這邊做資料過濾就可以。


#### `jQuery.ajax(url [, settings])`


| 參數 | 型別 | 說明 |
| -------- | -------- | -------- |
| url     | String     | 指定要進行呼叫的位址     |
|data	| Object	|要傳給 server 的 Key/value 值對|
|success	|Function	|Ajax 請求完成時 (必需是 success) 呼叫的 callback|




```javascript=
$(document).ready(function () {
  $("#searchUser").on("change", function (e) {
    let username = e.target.value; //取的輸入的內容
    $.ajax({
      url: "https://api.github.com/users/" + username,
      data: {
        client_id: "b9315bcd5a07fcd759d8",
        client_secret: "a2b698bf7e7c02f898197cf136d1a41f704ca8e4",
      },
      success: function insertProfile(user) {
        let obj = {};
        obj.avatar_url = user.avatar_url || "no data";
        obj.profile_url = user.html_url || "no data";
        obj.public_gists = user.public_gists || "no data";
        obj.public_repos = user.public_repos || "no data";
        obj.followers = user.followers || "no data";
        obj.following = user.following || "no data";
        obj.company = user.company || "no data";
        obj.location = user.location || "no data";
        obj.blog = user.blog || "no data";
        console.log(obj);
      },
    });
  });
});
```

顯示出來的過濾內容

![](https://i.imgur.com/0Xo8ovr.png)

### Profile放到DOM裡面

將取得的資料放到DOM裡面，使用`.html(profile)`。

```javascript=
var profile = `
<div class="card card-body mb-3">
<div class="row">
    <div class="col-md-3">
      <img class="img-fluid mb-2" src="${obj.avatar_url}">
      <a href="${user.html_url}" target="_blank" class="btn btn-primary btn-block mb-4">View Profile</a>
    </div>
    <div class="col-md-9">
      <span class="badge badge-primary">Public Repos: ${obj.public_repos}</span>
      <span class="badge badge-secondary">Public Gists: ${obj.public_gists}</span>
      <span class="badge badge-success">Followers: ${obj.followers}</span>
      <span class="badge badge-info">Following: ${obj.following}</span>
      <br><br>
      <ul class="list-group">
          <li class="list-group-item">Company: ${obj.company}</li>
          <li class="list-group-item">Website/Blog: ${obj.blog}</li>
          <li class="list-group-item">Location: ${obj.location}</li>
          <li class="list-group-item">Member Since: ${user.created_at}</li>
      </ul>
    </div>
</div>
</div>
<h3 class="page-heading mb-3">Latest Repos</h3>
<div id="repos"></div>
`;
$("#profile").html(profile);
},
```

### 取得repo資料

- 一樣透過網址也可以先觀察到json格式的資料，所以透過url來取得api的資料。

![](https://i.imgur.com/Qt2Cfit.png)

- data裡面的`sort`為排序的意思，asc代表正序，desc代表倒序。per_page代表要取得五筆資料。

- error為發現錯誤執行的function，jqXR為jQuery 1.5 版後，所有 jQuery 的 Ajax 方法 ($.get, $.post, $.ajax, ...) 都會返回一個 **jqXHR object**。

404為jqXHR.status的一種狀態。

![](https://i.imgur.com/N9N7amt.png)

- 使用到`setTimeout()`為輸入的內容沒有該使用者時，出現2.3s的錯誤警告，再自動清空輸入內容，與profile還有repo，增加使用者體驗。


```javascript=
$.ajax({
      url: "https://api.github.com/users/" + username + "/repos",
      data: {
        client_id: "b9315bcd5a07fcd759d8",
        client_secret: "a2b698bf7e7c02f898197cf136d1a41f704ca8e4",
        sort: "created: asc",
        per_page: 5,
      },
      error: function (jqXHR) {
        var msg = "";
        if (jqXHR.status == 404) {
          msg = `<div class = "alert alert-danger">
          Please enter again User does not exist</div>`;
        }
        $("#error").html(msg);

        setTimeout(() => {
          $("#searchUser").val("");
          $("#repos").html("");
          $("#error").html("");
          $("#profile").html("");
        }, 2300);
      },
      success: function insertRopo(repo_obj) {
        console.log(repo_obj);
      },
    });
```

印出來得到的repo就會是我們要的前五筆最新資料。

![](https://i.imgur.com/N6dLCda.png)


### Repo放到DOM裡

- 讀取連續五筆陣列資料，需要使用到`each`。這邊我遇到了一個錯誤，忘記了jquery語法，一直使用`foreach`，導致資料一直無法讀取。

```javascript=
$.each(repo_obj, function (index, repo) {
  $("#repos").append(`
  <div class="card card-body mb-2">
    <div class="row">
        <div class="col-md-6">
          <a href="${repo.html_url}" target="_blank" class="font-weight-bold">${repo.name}</a>
        </div>
        <div class="col-md-6">
          <span class="badge badge-primary">Stars: ${repo.stargazers_count}</span>
          <span class="badge badge-secondary">Watchers: ${repo.watchers_count}</span>
          <span class="badge badge-success">Forks: ${repo.forks_count}</span>
        </div>
    </div>
  </div>
  `);
});
```


## 遇到的錯誤

### 錯誤一

一直以為repo的dom是要新增一個`div`，在html才能夠放上去，所以直接在html加上了`div`，然後使用`.html()`更新repo的內容，發現只會出現一筆，所以換成了`append`，就可以成功跑出五筆。

但出現五筆後，每當我換一位使用者的名字時，他就會一直疊加資料，從五筆變成十筆，十五筆，非常可怕。

解決這個問題花了非常多的時間，後來才發現，放repo的`div`需要動態產生，動態產生時，就可以避免掉疊加的情況。

所以在profile的html裡，最後加上`<div id="repos"></div>`，就可以解決問題。

### 錯誤二

keyup會不停的被觸發，輸入可能五個字時他就會被觸發二十幾次，導致repo的內容會顯示超過五筆，Error提醒也會不停被觸發，目前還在釐清這個問題。

但是，換成change之後，等待使用者輸入完成後，才觸發，就可以解決這個問題。

## 參考文章

[jQuery Ajax](https://www.fooish.com/jquery/ajax.html)