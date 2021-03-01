## 學習到的知識點

### CSS

- `disable`
- `!important`
<!--more-->

### JS

- `.hasClass`，檢查被選擇的元素**是否包含**指定的`class`。
- `.text`
- `.removeClass`

## 簡介

[Demo](https://hff2.github.io/My-Projects/Tic_Tac_Toe/index.html)

- 判斷兩方誰先連線
- 需兩方輪流操作點擊後新增圈圈與叉叉
- 判斷是否合局

![](https://i.imgur.com/KPMiLxU.png)

## HTML

### 結構

結構十分簡單，利用`ul`和`li`來建立。

最下面新增一個**清除**的按鈕。

```html=
<div id="container">
    <header>
        <h1>Tic Tac Toe</h1>
    </header>
    <ul id="board">
        <li id="spot1">+</li>
        <li id="spot2">+</li>
        <li id="spot3">+</li>
        <li id="spot4">+</li>
        <li id="spot5">+</li>
        <li id="spot6">+</li>
        <li id="spot7">+</li>
        <li id="spot8">+</li>
        <li id="spot9">+</li>
    </ul>
    <div class="clearfix"></div>
    <footer>
        <button id="reset">Reset Game</button>
    </footer>
</div>
```

## CSS

### disable 按鈕禁用

HTML button disabled 是用來讓按鈕禁止使用的，簡單來說當你的網頁有按鈕出現，卻又不希望使用者按下按鈕，就可以使用 disabled 這樣的語法，讓按鈕功能失效。

```html=
<input type="button" disabled="disabled" value="這個按鈕不能使用">
```

### `!important`的用法

預設狀態下，CSS 採用順序為：

style 定義 > class 定義 > default 定義

如果在 class 內的特定項目後面加上`!important`時，則採用順序會變成

class 內有(!important)項目 > style 定義 > class 定義 > default 定義。

## JS

[完整 Code](https://github.com/hff2/My-Projects/blob/tic-tac-toe/Tic_Tac_Toe/script.js)

### 如何在`li`被點擊時出現反應?

![](https://i.imgur.com/a2ChBcm.png)

```javascript=
$(document).ready(function () {
    var x = "x";
    var o = "o";
    var turns = 0;

    $("#board li").on('click',function(){
        alert("clicked");
    })
});
```

### 如果第九次沒有出現贏家?

平手的話，就重新開始。

turn 也歸零。

```javascript=
else if(turns == 9){
    alert('Tie Game');
    $('#board li').text('+');
    $('#board li').removeClass('disable');
    $('#board li').removeClass('o');
    $('#board li').removeClass('x');
    turns = 0;
```

### 可以重複切換圈圈叉叉怎麼辦?

加上 CSS 屬性`disable`，就可以使按鈕禁止使用。

```javascript=
else if($(this).hasClass('disable')){
    alert('This spot is already filled');
}
```

### 點擊`li`時，如何出現圈圈與叉叉?

每當點擊時，次數要+1。

增加`text`( 圈圈或叉叉 )與`class disable`。

而每次點擊完圈圈與叉叉後，都需要判斷是否連線了，如果連線了，就清空所有使用者添加的元素，回到 reset 狀態。

```javascript=
else if(turns%2 == 0){
    turns++;
    $(this).text(o);
    $(this).addClass('disable o');
    if(spot1.hasClass('o') && spot2.hasClass('o') && spot3.hasClass('o') ||
        spot4.hasClass('o') && spot5.hasClass('o') && spot6.hasClass('o') ||
        spot7.hasClass('o') && spot8.hasClass('o') && spot9.hasClass('o') ||
        spot1.hasClass('o') && spot4.hasClass('o') && spot7.hasClass('o') ||
        spot2.hasClass('o') && spot5.hasClass('o') && spot8.hasClass('o') ||
        spot3.hasClass('o') && spot6.hasClass('o') && spot9.hasClass('o') ||
        spot1.hasClass('o') && spot5.hasClass('o') && spot9.hasClass('o') ||
        spot3.hasClass('o') && spot5.hasClass('o') && spot7.hasClass('o')
    ){
        alert('Winner: O');
        $('#board li').text('+');
        $('#board li').removeClass('disable');
        $('#board li').removeClass('o');
        $('#board li').removeClass('x');
        turns = 0;
    }
}
```

## 參考文章

[# css !important 用法以及 CSS 樣式使用優先級判斷](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjIxsmxzI7vAhU6K6YKHfweDRcQFjABegQIAxAD&url=https%3A%2F%2Fwww.itread01.com%2Fcontent%2F1535990526.html&usg=AOvVaw1dNqiZIwP7NkP-BJI377J0)

[:disabled - CSS（层叠样式表） | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:disabled)
