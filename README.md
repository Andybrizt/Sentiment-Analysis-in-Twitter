# Sentiment-Analysis-in-Twitter


## Machine Learning-訓練Naive Bayes Classifier Model，預測Twitter發文是正面還是負面[kaggle]
>  在機器學習中，單純貝氏分類器是一系列以假設特徵之間強（樸素）獨立下運用貝葉斯定理為基礎的簡單機率分類器。-Wikipedia

Google kaggle資料科學競賽平台中，有許多真實Twitter用戶PO文的dataset，非常適合拿來做情感分析，需多企業也會拿來做仇恨言論分析。

大多數的文字情感分析(**Sentiment Analysis**)是使用Naive Bayes classifier。

Naive Bayes classifier是相當知名的分類性模型之一。其實早在五十年前便已經被拿來分類文本用，在政治、科學、文學領域有高性能的表現。

五十年前?沒錯，這個模型確實是源自於古典數學，貝氏定理。

現在得力於電腦性能提升，靈活度更是大大增加，可控性極強。

## Naive Bayes classifier的特性:

1.源自於古典數學，引數簡單

2.訓練時間迅速，只需要消耗線性時間

3.如果變量獨立，樸素貝葉斯分類器只需少量訓練數據，同時性能比Logistic回歸更加優秀

## 核心算法

![](https://cdn-images-1.medium.com/max/2000/1*mxMR1iQulYMaAqyvw8dhWg.png)

「條件機率」就是核心

在機器學習裡，為了方便理解，可以直接把:

Y當成類別

X就是特徵

這裡大家有個大概了解即可，我會在接下來的實作中講解

## 實作Twitter情感分析

**首先，先讀入dataset**

dataset網址:[https://www.kaggle.com/paoloripamonti/twitter-sentiment-analysis](https://www.kaggle.com/paoloripamonti/twitter-sentiment-analysis)

接著，大概看一下dataframe:

![](https://cdn-images-1.medium.com/max/2000/1*bKrJsXAklfYZZrMkhwgABQ.png)

tweet欄位中，都是從真實人類在Twitter上的PO文用爬蟲爬下來的，然後把用戶的帳號ID都用user取代保護隱私

label欄位中的0代表正面言論，1代表負面言論

丟掉一些不重要的column，這裡我們丟掉id

然後，我們用圖表方式呈現dataframe中是否有nulll值

![一片白色，就表示沒有任何null值或缺值](https://cdn-images-1.medium.com/max/2000/1*hWmX6E1pNmlJiTnYEhfY0Q.png)

查看正面(0)和負面(1)言論的數量

![資料不平衡](https://cdn-images-1.medium.com/max/2000/1*0-DW9UnrROWsXwOLDa_NqQ.png)

看起來正面言論的數量遠大於負面言論，這是一個**資料不平衡**的現象。

至於資料不平衡和如何解決我會在另一篇文章闡述

## 產生文字雲

文字雲可以讓我們快速掃描正面和負面言論常出現的字(word)

**正面**

![](https://cdn-images-1.medium.com/max/2000/1*mJCTbXcYl5VEkvgPOsQBPg.png)

![Positive word cloud](https://cdn-images-1.medium.com/max/2830/1*JFoXJbBOCwUE_tCO1TBdcA.png)

不意外，happy、love、life、today、friend…etc都代表正面詞

**負面**

![Negative word cloud](https://cdn-images-1.medium.com/max/2898/1*Iab1HhsD8IdjxwLoiFTHxQ.png)

racist、hatehate、racism可以理解，那libtard、sjw是什麼?

其實跟美國文化也有關

libtard:沒有一個統一的翻法，大略的意思是指不現實或紙上談兵、過度理想的左翼分子

sjw: Social Justice Warrior，帶有貶義

從Twitter上也可以知道國外局勢呢!

## 清洗資料

**移除標點符號**

標點符號是包含哪些呢?

    !"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~

在這個實作中，我們不考慮這些標點符號

可以用以下迴圈移除

![](https://cdn-images-1.medium.com/max/6064/1*d63ULRDOOMJauJ4x1-ioGw.png)

移除stop word

為節省空間和提高效率，在自然語言處理數據會過濾掉某些字或詞

![credit:[ResearchGate](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.researchgate.net%2Ffigure%2FList-of-Stopwords-in-Text-Mining-Library-of-R_fig8_318138987&psig=AOvVaw391txiCz5RvMbt3lkvlKB2&ust=1597822084002000&source=images&cd=vfe&ved=0CA0QjhxqFwoTCLjZ8KOdpOsCFQAAAAAdAAAAABAD)](https://cdn-images-1.medium.com/max/2000/1*R1NmayfziRv8QKKUw4dt_w.png)

![](https://cdn-images-1.medium.com/max/4312/1*dJ_AuW96pwAQy_qRNPfWyw.png)

其實就是一些主詞、受詞、代詞、動詞

## Feature extraction

### TOKENIZATION

* **tokenizing** 令牌化 :對每個可能的 詞令牌(token) ，分成字串並給予id。通常使用空格或標點符號作為token separators

* **counting** 統計token數: 每個文檔中token的出現數量

上述的方法都是處理文字的特徵工程常用的流程

而sklearn中的CountVectorizer可以同時處理上述兩個工作

這裡給個範例:

1.建立一個CountVectorizer object

    **from** **sklearn.feature_extraction.text** **import** CountVectorizer
    sample_data = ['This is the first paper.','This document is the second paper.','And this is the third one.','Is this the first paper?']
    
    vectorizer = CountVectorizer()

2.fit_transform(trainData)進行fit，再進行transform

    X = vectorizer.fit_transform(sample_data)

3.看看有那些特徵

    print(vectorizer.get_feature_names())

    輸出:
    ['and', 'document', 'first', 'is', 'one', 'paper', 'second', 'the', 'third', 'this']

4.轉成矩陣

    print(X.toarray())

    輸出:
    [[0 0 1 1 0 1 0 1 0 1]
     [0 1 0 1 0 1 1 1 0 1]
     [1 0 0 1 1 0 0 1 1 1]
     [0 0 1 1 0 1 0 1 0 1]]

第一列0011010101分別對應第3點的特徵

first、is、paper、the、this都有出現一次，所以為1

其他以此類推

## 整合成Pipeline

資料科學和機器學習中，Pipeline可以節省時間，並在下次遇到類似問題不必再重新建立流程，直接把舊的拿來調整即可

著手把下面三個流程

    *(1) remove punctuation
    (2) remove stopwords
    (3) PERFORM COUNT VECTORIZATION*

整合成Pipeline

來寫一個message_cleaning函式來一次過清洗資料

![](https://cdn-images-1.medium.com/max/8192/1*ScofJ52Oqne79cSO8dOrVA.png)

接下來使用CountVectorizer(tokenizer)利用清洗好的文字產生token，並用toarray()轉換成詞頻矩陣。

最後，擬合(fit)

![](https://cdn-images-1.medium.com/max/8192/1*b7gUtRW7Jck31FMZwYMJ3Q.png)

## 訓練模型

![](https://cdn-images-1.medium.com/max/5392/1*qQhST7Yq1Gq-nG6DOOVHOQ.png)

我在這裡使用的是MultinomialNB分類器

為什麼呢?因為多項式MultinomialNB比較適合離散式特徵，例:上面的token計數就是

![](https://cdn-images-1.medium.com/max/3568/1*YNd2spQKnk-9MCu5MnqDJw.png)

## 觀察模型效能

我們使用混淆矩陣來看看訓練出來的模型效能

![](https://cdn-images-1.medium.com/max/4032/1*sysnn0aapUyP3tnpWkLs5g.png)

![confusion matrix](https://cdn-images-1.medium.com/max/2000/1*_NWCB23CHy48JUzy9MGFiw.png)

confusion matrix用heatmap印出比較直觀

縱軸是測試資料

橫軸是預測結果

可以參考此圖

![](https://cdn-images-1.medium.com/max/2000/1*NSVob4rF_S_ST5NFsCuRxQ.png)

True Positive:預測結果為真，實際值也為真

True Negative:預測結果為假，實際值也為假

False Positive:預測結果為真，實際值卻為假

False Negative:預測值為假，實際值卻為真

當然，TP與TN越高越好。

由此可知，我訓練的模型偵測正面言論的準確率蠻高的(confusion matrix左上角)，至於其他的狀況就算普通。為什麼呢?因為一開始的dataset是不平衡的，正面言論遠比負面言論多。

來檢查一下報告

![](https://cdn-images-1.medium.com/max/4024/1*exMZH-ckCIMo-e76-IWCLw.png)

![](https://cdn-images-1.medium.com/max/4168/1*j_3LEEDHftMcgxA-vrA7vA.png)

很明顯，0的精準度還是蠻高的，但是1的精準度較差

相信把不平衡的問題解決，精準度可以提升

若想要把文字丟進去給他預測，可以參考我的別篇文章。
