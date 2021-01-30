---
title: PR 是什麼? git clone 和 git pull的差別 ?
author: Phoebe
tags: Git
categories: Git
date: 2021-01-10 09:15:44
---
## PR是什麼?

Github上面有很多開源專案，當我們想要幫忙修改內容或是添加新功能時，一開始不需要經過原作者同意就能下載使用。

做好了之後，再發個通知跟作者說我做好了，請你看一下要不要做使用(Merge)。
<!--more-->

發個通知就是Pull Request(PR)。

## 如何發PR?

### 方法一

1. 可以先Fork一分到自己的帳號下，可以獲得完整的權限，隨便你改。

![](https://i.imgur.com/XFyKDp4.png)

2. 改完之後，在推回(git push)自己的帳號
3. 然後"發通知"告訴原作者，我對你的專案做了一些事情，請你看一下。
4. 原作者覺得有幫助時，就會把我們做的修改合併(merge)到他的專案。


發出通知，就是Pull Request(PR)，請原作者看看我的修改，作者覺得可以時，就把我的請求(Request)拉(Pull)回去到他的專案裡。

### 方法二

1. 可以複製code下的ssh連結，在終端機打上` git clone `+複製的連結。

![](https://i.imgur.com/6Zi3MKk.png)

2. 建立新的branch

![](https://i.imgur.com/jxVHGJv.png)

3. 檢查branch是否存在

![](https://i.imgur.com/61N7tBZ.png)

5. 切換branch，`git checkout ...`

![](https://i.imgur.com/UIjjZu9.png)

7. `git add .` ，`git commit -m ...`
8. `git push`

![](https://i.imgur.com/WsUjbpz.png)

9. 到github pull-request頁面建立pull-request。
10. 選擇自己創建的branch
11. 發出pull-request
12. 等待被merge

## 當PR被Merge後，要如何發下一個 PR？

1. 切回main branch
2. 使用`git pull`下載最新版本
3. 創建新的branch
4. `git push`，完成更新。

## git clone與git pull的差別?

git clone 是當我第一次看到別人的專案，想要下載到我電腦裡執行的指令。

git pull是下載之後，想要更新專案的最新內容，就要使用pull。

簡單來說，`git clone`只會用在第一次，其他的更新都是使用`git pull`。