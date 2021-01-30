---
title: 在Windows 上安裝 WSl
author: Phoebe
date: 2020-11-20 12:27:43
tags: WSL
categories: Window
---
# 在Windows 上安裝 WSl

由於安裝過程遇到許多問題，在此做紀錄。

[官方文件](https://docs.microsoft.com/zh-tw/windows/wsl/install-win10)
<!--more-->
### (一)系統管理員身分(滑鼠右鍵按下)，開啟 PowerShell 並執行。執行完成後跳出100%完成。

> dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

![](https://i.imgur.com/Si4PFfb.jpg)

### (二) 更新到 WSL 2 

<font color="red">注意自己的版本是否符合。</font>
* 若為 X64 系統： 版本 1903 或更高版本，含 組建 18362 或更高組建。
* 若為 ARM64 系統： 版本 2004 或更高版本，含 組建 19041 或更高組建。
* 低於 18362 的組建不支援 WSL 2。

(檢查您的版本及組建號碼，請選取 [Windows 標誌鍵 + R]、輸入 winver ，然後選取 [確定]。 )

![](https://i.imgur.com/9ym5go6.png)

##### 我遇到的錯誤：
沒有自動跳出重新啟動的選項。

![](https://i.imgur.com/tcm5ErH.jpg)

想要確認自己是否成功將WSL升級成WSL2的話，可以參考下方文章進行檢查：
https://samiouob.github.io/2019/06/17/WSL2/

### (三)啟用虛擬機器功能

在安裝 WSL 2 之前，須啟用 虛擬機器平台 選用功能。


### (四)下載 Linux 核心更新套件

[WSL2 Linux 核心更新套件 (適用於 x64 電腦)](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)


### (五)將 WSL 2 設定為預設版本

開啟 PowerShell，然後執行下列命令，，以將 WSL 2 設定為預設版本
> wsl --set-default-version 2
#### 我遇到的問題：

![](https://i.imgur.com/GcEw3Q2.jpg)


### (六)安裝 Linux 發行版本

開啟 Microsoft Store，然後選取 Linux 發行版本。我是安裝Ubuntu-18.04版本。

![](https://i.imgur.com/s5Aa1eK.png)

:::success
在這邊我遇到了Windows10的Microsoft Store本機端消失，導致我沒辦法下載 Ubuntu，就算在官網也無法下載。

網路上遇到此問題的人也不少，但都沒有精準回答到問題。

最後，我找到一部影片教學十種方法修復Microsoft Store問題，最後得以成功下載。

https://www.youtube.com/watch?v=PWGNL7cKoYU&t=184s
:::

### (七) 設定新的發行版本

我們必須為新的 Linux 發行版本設定使用者<font color="red">帳戶</font>和<font color="red">密碼</font>


![](https://i.imgur.com/h9DoQ5q.jpg)

這邊在安裝時出現了問題，後來使用這網站的方法得以解決。
https://www.jianshu.com/p/5f7b83ca3952

### 安裝 Windows 終端機

[直接裝起來](https://docs.microsoft.com/zh-tw/windows/terminal/get-started)

### 安裝Bash

在6分14秒後有一些Bash的教學可以學習。
https://www.youtube.com/watch?v=1ap3hL-UR9I&t=252s

### 安裝zsh

安裝過程參考了這篇文
https://www.jianshu.com/p/5f7b83ca3952


### WSL是什麼?

![](https://i.imgur.com/3A2DftT.png)

Windows Subsystem for Linux，一套能夠運行在window系統上面的Linux核心。

### Bash 是什麼?

![](https://i.imgur.com/l89JPMN.png)
Bash，Unix shell的一種，一個命令處理器，通常執行於文字窗口中，並能執行用戶直接輸入的命令。能夠從檔案中讀取命令，這樣的檔案稱為指令碼。

