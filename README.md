# Sentiment-Analysis-in-Twitter

## 如何在 medium 分享程式碼(2020/5/15 更新）

準備在 medium 寫筆記時，發現貼程式碼的方式其實沒有寫 markdown 那麼直覺，所以寫了這篇文章記錄一下網路上找到的分享方式。

給忙碌的人看的版本：

 1. [方便的方式](#43b7)：在 medium 編輯頁面按下 **Ctrl + Alt + 6（windows）、Cmd + Option + 6 (mac OS)。**

 2. [實用的方式](#7dba)：用 [**Gist ](https://gist.github.com/discover)**嵌入、[**codepen](https://codepen.io/) **嵌入。

 3. [美觀的方式](#3b4d)：用程式碼圖片產生器（[**Carbon](https://carbon.now.sh/)**、[**PolaCode](https://marketplace.visualstudio.com/items?itemName=pnp.polacode)** in vscode）

進入正文：

## **1. 最方便：medium 內建功能**

在 medium 的 story 撰寫頁面中，依照您目前現在的作業系統按下：

windows: **Ctrl + Alt + 6**

mac OS: **Cmd + Option + 6**

    按完後就會出現這個灰色的框框

這是目前最方便的方式，但可惜的是他**不支援語法 highlight **的功能，而且縮排的時候會有點卡卡的。

    console.log("Hello world");

    function Test(params){
      return params
    };

## 2. 最實用：嵌入 Gist 的連結

[Gist](https://gist.github.com/discover) 是 Github 所提供，其中一項它的服務就是儲存程式碼的片段。所以將我們想要分享的程式碼片段存到 Gist 中，並且生成 url 嵌入到 medium 的頁面上，就能達到我們想要的分享功能了。

首先，先進到 [Gist](https://gist.github.com/discover) 的首頁並登入（和 github 使用同一個帳號），會看到以下頁面：

![Gist 登入後的樣子](https://cdn-images-1.medium.com/max/2062/1*Z8uxUrQDEmd4UbjkXQN8NA.png)

點擊右上的「+」，就會進到下面新增程式碼片段的頁面：

![](https://cdn-images-1.medium.com/max/2066/1*6cWcuf1YjzCc6sM79S5bGg.png)

填完程式碼片段描述、檔案名稱、程式碼片段內容後按下 Create public gist後，接下來會到該程式碼片段的頁面，按下下圖紅色圈選處的地方來產 medium 可以嵌入的 url：

![類型記得要選 share !](https://cdn-images-1.medium.com/max/2230/1*9PwvcrAu9WWYPoHxIYULHA.png)

複製好 url ，接著在 medium 的編輯頁面中，選擇 Add an embed 後，貼上剛剛複製的 url ，按下enter 後就完成啦：

 <iframe src="https://medium.com/media/28f6cf991e45a2a2a6d1fff2df448f6e" frameborder=0></iframe>

完美地支援語法 highlight，且若之後如果程式碼有變動直接去更改，嵌入的頁面也會同步更新，但如果文章程式碼片段很多，這個方式有點麻煩。另外後續如果文章變多，程式碼片段的管理也是一個問題。

## Codepen 嵌入

要在 medium 分享 codepen 專案十分簡單，直接在 medium 的編輯頁面中，選擇 Add an embed 後，輸入 codepen 的專案連結就可以了！

 <iframe src="https://medium.com/media/055906de2ce16f24b3a816ad7dadc343" frameborder=0></iframe>

## 3. 美觀的方式

使用線上產生程式碼片段圖片的服務 [Carbon](https://carbon.now.sh/)，可以產生圖片，也可以像Gist 一樣產生可嵌入的 url：

 <iframe src="https://medium.com/media/23a5dfd3387adb45ba2c3c197ce6f16f" frameborder=0></iframe>

如果使用 vscode 的話，也有 extension [PolaCode](https://marketplace.visualstudio.com/items?itemName=pnp.polacode) 讓您快速的在現有的程式碼中產生圖片：

![](https://cdn-images-1.medium.com/max/2116/1*Z0EJV3nf4pnR-P2lICCjyw.png)

這是目前所有方式中我認為最美觀的，但是如果要更改裡面的內容，就要再重新擷取並上傳一次圖片了。另外也因為是圖片，沒辦法直接從裡面複製程式碼。

## So…

我覺得上面的方式相比直接寫在 markdown 都相對麻煩很多 😭 😭，希望 medium 也能支援類似 markdwon 的程式碼語法啊~~🥢💥🍚
