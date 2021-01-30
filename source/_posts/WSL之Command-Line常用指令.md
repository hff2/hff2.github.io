---
title: WSL之Command Line常用指令
author: Phoebe
tags: WSL
categories: Window
date: 2020-11-25 23:03:18
---
### cd:切換資料夾

![](https://i.imgur.com/bFDrP8T.png)



打開wsl預設會在使用者目錄(家目錄)，會是/home/[使用者名稱]，我的目錄就是/home/phoebe。
<!--more-->
![](https://i.imgur.com/zrtbSb5.png)




### pwd:顯示目前目錄



![](https://i.imgur.com/O8y05ot.png)

### cd ~:回到家目錄

![](https://i.imgur.com/D2JAni1.png)


### ls:看資料夾下面有什麼檔案

* ls      查看資料夾內的檔案
* ls -l   查看資料夾內的檔案和詳細資料
* ls -al  查看資料夾內的隱藏檔案和詳細資料

![](https://i.imgur.com/Vw30wqL.png)


### /mnt/c:進入C槽

WSL預設把Windows的C:槽掛在/mnt/c，D:槽掛在/mnt/d。

如果在桌面開一個project資料夾，WSL中就會在/mnt/c/Users/user/Desktop/project。

先從Linux資料夾跳出後，到C槽裡的git資料夾。

![](https://i.imgur.com/QyW4HHb.png)


### mkdir:新增資料夾

![](https://i.imgur.com/1z0lxoS.png)

### touch:建立檔案

![](https://i.imgur.com/gWl4vOl.png)

### cat:讀取檔案內容

![](https://i.imgur.com/ES0Bqgt.png)

### mv:可以用來移動檔案或重新命名檔案：
* 移動檔案位置

mv /mnt/c/Users/user/git/1121.txt ~/1121.txt

* 將 1120.txt 改名成 1121.txt

mv 1120.txt 1121.txt

![](https://i.imgur.com/i7id1xy.png)


### cp: 用來複製檔案或資料夾

Test資料夾出現1120.txt

![](https://i.imgur.com/k7xKHZ4.png)

### rm：remove 刪除目錄或檔案
![](https://i.imgur.com/3FxUZ5v.png)

### rm -i ：刪除之前會詢問
如果要刪除建議使用這個參數，可以避免誤刪。
![](https://i.imgur.com/QL4rnMr.png)

### rm -f :刪除整個資料夾(徹底刪除)
強制刪除檔案或目錄，不會有警告，請小心使用。


### 後記

使用cmder時，遇到許多問題，每次開始前都要輸入wsl才能開始正常使用指令，別人安裝好都可以直接運行ls，car，touch...等指令，但我的就是無法...後來發現Microsoft商店有介面超好看的Terminal，而且可以開不同的分頁，可以運行cmd,powershell,wsl都非常方便。

遇到Microsoft Terminal問題時，網路上的教學也比Cmder來的多，雖然花了很多時間研究怎麼樣弄好Cmder，後來也成功運行，但Terminal還是方便多，所以還是直接換過去了XD。