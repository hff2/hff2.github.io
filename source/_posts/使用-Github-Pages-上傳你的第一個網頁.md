---
title: 使用 Github Pages 上傳你的第一個網頁
author: Phoebe
date: 2020-12-3 13:29:57
tags: Git
categories: Git
---
## 步驟

1. 初始化資料夾

![](https://i.imgur.com/Bveok8Y.png)
<!--more-->
2. 建立資料夾

![](https://i.imgur.com/R9pDD1b.png)

3. 將變更內容註冊到索引上

![](https://i.imgur.com/P4YnSWK.png)

1. 將索引的內容提交至本機儲存庫上

![](https://i.imgur.com/Ht6Tv4L.png)

5. 輸入指令`code .` 打開vscode編輯

![](https://i.imgur.com/FJLUuLn.png)

vscode檔案出現M代表編輯過，需要重新將內容註冊到索引上。

![](https://i.imgur.com/Cys7bV4.png)

6. 對他重新進行add和commit指令。

![](https://i.imgur.com/jWnQzo4.png)

vscode顯示也會取消

![](https://i.imgur.com/OGNR5QL.png)

7. 建立分支，切換分支

![](https://i.imgur.com/19EgRbG.png)

![](https://i.imgur.com/uUcScBh.png)

8. 在Github上建立一個Repository，照著已存在的檔案操作。

![](https://i.imgur.com/wrjX9iA.png)

9. 複製貼上

![](https://i.imgur.com/ZeGmQGr.png)

![](https://i.imgur.com/LmJKSaz.png)


10. 成功上傳

開啟github


![](https://i.imgur.com/6cKmpBU.png)

[網頁連結](https://hff2.github.io/test/)

## 遇到問題 1

![](https://i.imgur.com/h4Ybd0U.png)

出現這個錯誤的常見原因為三種:

* 本地端git目錄沒有檔案
* 本地端add後未commit
* git init錯誤

我認為我是第三種，我的處理的方法為，輸入指令

1. git config user.name "someone"
2. git config user.email "someone@someplace.com"
3. git add .
4. git commit -m "some init msg"

在git創建項目時出現，是因為在創建git文件夾的時候訊息不完善導致的。

重新認識了我的帳號之後，就可以成功上傳。


## 遇到問題 2

github page跑不出來

後來更改了page設定，在settings裡做修改。

![](https://i.imgur.com/I7eBftv.png)

## 遇到問題 3

GitHub以Main取代Master做為新Git儲存庫預設名稱。

![](https://i.imgur.com/wrjX9iA.png)

這行指令中的git branch -M main，就是將Main作為預設存庫的名稱。

原因是為響應黑人平權運動，GitHub宣布從2020的10月1日起改變新Git儲存庫的預設命名，以main來取代原本的master。

不過這項變更並不會影響現有儲存庫的名稱。開發人員也可以不要變更，隨時到設定區，把個人、組織和公司的新儲存庫預設命名從main改成別的!

[參考連結](https://www.ithome.com.tw/news/140094)