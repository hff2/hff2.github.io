---
title: Git基礎介紹，常見指令
author: Phoebe
tags: Git
categories: Git
date: 2020-12-04 22:36:33
---

## Git是什麼?
![](https://i.imgur.com/84NmYzt.jpg)

* 主要是專案開發時用來做的版本管理工具，編輯者可以將檔案變更的歷程儲存起來，隨時參考、取得過去的歷史紀錄。被稱為版本控制系統。

<!--more-->

* 早期的版本控制管理系統，可以讓多位編輯者共享的檔案儲存庫，以及編輯者自己作業要使用的檔案。但這樣要查看變更時，就需要一直登入伺服器查看。

* 而Git 則是將共享儲存庫的副本儲存在編輯者的電腦裡，也就是所謂的本機儲存庫。有了本機儲存庫，不需要反覆登入伺服器去查看歷史變更資料，效率就可以提高。

## Git重要名詞

### 共享儲存庫
多位編輯者所共享的儲存庫，可以在這裡共享由各自本機儲存庫上傳至共享儲存庫的變更。
### 本機儲存庫
編輯者自己電腦的儲存庫，編輯者透過
1. `clone` 複製
將共享儲存庫複製下來使用，然後再將本機儲存庫的變更，透過
2. `push` 上傳
傳到共享儲存庫。
若要從共享儲存庫上讀取其他編輯者所上傳的變更，就用
3. `pull` (下載)

### 工作目錄
編輯者實際編輯的檔案。透過`Checkout`指令可以切換到其他分支來編輯檔案，並作為特定版本。

### 索引(或暫存目錄)
暫時存放工作目錄的地方。編輯者透過add指令把工作目錄變更註冊到索引上。而被註冊到索引上的變更，可透過`commit`(提交)上傳至共享資料庫。
## 建立SSH憑證
GitHub提供了HTTPS與SSH（Secure Shell）兩種通訊方式讓我們的Git Client與之連線。我們選擇使用SSH連線。

### ssh key是什麼?
![](https://i.imgur.com/mDfrCb1.png)


透過 Public Key Authentication 的方式，可以不需輸入密碼就透過 SSH 進入你的遠端主機(Github)。

Public Key Authentication 是透過非對稱金鑰的方式來驗證 SSH 登入。所謂的非對稱金鑰是指，我們會產生兩把鑰匙：一把稱為公鑰（Public Key）、另一把稱為私鑰（Private Key），其中一個用來加密資料，就必須拿對應的金鑰解密才能得到原本的資料。

1. 建立Windows的SSH金鑰:

```
cd "c:/users\uesr\git\usr\bin\"
ssh-keygen -t rsa -b 4096 -C "你的Email"
```
產生的金鑰檔案會存入 C:\Users\登入帳號.ssh 資料夾

私鑰：id_rsa
公鑰：id_rsa.pub

2. 複製公鑰 id_rsa.pub 的內容到系統剪貼簿

自動開啟vscode，key就會顯示在上面。

```
vscode id_rsa.pub
```

3. 登入 GitHub，按【Settings】，找到【SSH and GPG keys】，按【New SSH Keys】
4. 輸入辨識用的名稱並貼入id_rsa.pub的內容後按【Add SSH Key】
5. 建立儲存庫(Repository)並複製其SSH協定的Repository URL


我一開始安裝putty，結果要上傳靜態網頁時出現了問題!後來才發現不能使用putty，使用上述方法所有問題都迎刃而解。


## 常用的指令介紹
### init
git 儲存庫的初始化，用於建立新的儲存庫。
* mkdir test，創建資料夾 

![](https://i.imgur.com/suvKnOJ.png)

* git init，資料夾做初始化

![](https://i.imgur.com/uXxXxIc.png)



### clone

複製Git儲存庫，將遠端儲存庫複製到本機儲存庫上。
* `git clone 要clone網址`

### add
將變更內容註冊到索引(暫存區)上，並作為提交對象，且尚未被傳到儲存庫上。


![](https://i.imgur.com/DVfJyvX.png)



* `git add .`把目前的工作目錄上的所有檔案註冊在索引上。
* `git add -A`不只限於目前的工作目錄，而是包含整個工作目錄的檔案都會在索引上。若檔案被刪除，就不會被註冊。



![](https://i.imgur.com/OySPOgm.png)

### commit
將索引的內容提交至本機儲存庫上。

* `git commmit -a` 可以省去索引註冊的程序，直接將檔案提交到儲存庫。
* `git commit -m "修正的內容"` 給存檔一個名稱，進行存檔。

![](https://i.imgur.com/wVTZzbY.png)





### status
顯示工作目錄上的檔案狀態，確認版本控管檔案以及已註冊於索引的檔案。

![](https://i.imgur.com/AGacIuu.png)

### ls
顯示該資料夾底下的文件

### log

顯示分支的變更歷程

### branch

操作分支
* `git branch` 查看目前分支與既存分支
* `git branch dev` 命名branch
* `git branch -m` 變更分支名稱
* `git branch -M` 變更分支名稱。當所設定的分支名稱已經存在，則強制使用變更的名稱。
* `git checkout -b` ，新增branch + checkout過去。

![](https://i.imgur.com/KbDRXVy.png)


![](https://i.imgur.com/8TEJIQn.png)


:bulb: Github把預設分支換成了**main**，而git預設的branch還是**master**，可以用`git branch -m main`修改主要 branch 名稱為main，然後再用`git checkout main`進行開發。


### checkout

更換工作目錄

![](https://i.imgur.com/zqQAuf3.png)


### merge
將目前分支與特定分支合併
1. master裡有Hello.txt檔案
2. 新增dev裡有 1125.md檔案
3. 在master裡有Hello2.txt檔案
4. git merge dev，成功合併。

![](https://i.imgur.com/SHfewGi.png)
![](https://i.imgur.com/fPUk7w9.png)


:bulb: 如果不小心merge錯誤，可以使用`git reset commit-hash`回到合併前的分支，再下`git push -force`，強制刷新github狀態，但`git push -f`多人協作比需少用，容易覆蓋他人檔案。


### push
將變更過歷程的儲存庫傳送到共享儲存庫


## 想刪除Repository 裡的資料夾?

[參考文章](https://www.zhihu.com/question/20418177)

```
git rm -r --cached test  #--cached不會把本地的test資料夾删除
git commit -m 'delete test dir'
git push 
```