---
layout: default
title: Data Type 資料型別
parent: JavaScript 入門核心概念
nav_order: 2
permalink: date-type.html
---
# Data Type  資料型別

所有的程式語言都具有資料型別 (data type) 和資料結構 (data structure) 的設計：

- Data type 是用來告訴電腦系統的編繹器 (compiler) 如何處理這組資料，如果不當使用資料型別，當程式執行時就會發生錯誤；
- Data Structure 是 data 的集合體，把資料用某個結構組織起來，才可以做更有效的讀取，若要設計有效率的程式，就需要好好思考資料結構的設計；

依語言的性質 data type and structure 的設計會有差異。在 JavaScript 的 ES6 標準裡，一共定義了以下 7 種資料型別 (data type)：

[Untitled](Data%20Type%20%E8%B3%87%E6%96%99%E5%9E%8B%E5%88%A5%20896b74e511eb443fa73caa29f25eac27/Untitled%20Database%20a3885edf562648d98b0693a891159c00.csv)

上述中，前六個被稱為「基本型別 (primitive type)」，與物件型別做區分。

# undefined

我們來認識一下 `undefined` 。在下面的範例中，我宣告了一個變數 `myVariable`，但是沒有賦值，這時候當我們呼叫它，你會發現回傳值是 `undefined`：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/6995/pasted_image_0__5_.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/6995/pasted_image_0__5_.png)

請注意，程式並沒有發生錯誤，它只是回傳`undefined`，表示變數內容未經定義。在以下的例子，當你去呼叫一個不存在的變數時，才會發生錯誤：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/6996/pasted_image_0__6_.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/6996/pasted_image_0__6_.png)

# 檢查資料型別

你可以使用 `typeof` 來檢查資料的型別，例如：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4592/image_3.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4592/image_3.png)

# 型別強制轉換 (coercion)

把兩種型別放在一起時，會發生什麼事？

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4593/image_4.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4593/image_4.png)

回傳值是 `12`！JavaScript 是一個寬鬆且聰明的語言，它會自己去猜測你想要表達的意思是什麼，因此，它在執行過程中，將變數 `a` 強制轉換成字串，你可能預期回傳值是數字 `3`，卻得到了字串 `12`。

# 在字串裡嵌套變數

現在，試著想像你在寫一個遊戲，玩家的分數儲存在 `userScore` 這個變數中，你需要印出一句話：「你這回合的分數是：XX」，有兩個方式可以做到這件事：

# **方法一：使用 + 號**

傳統方法是使用加號 (`+`)：

```
let userScore = 10257
let scoreNotificationStart = 'Your score is: '
let scoreNotificationEnd = ' in this round.'
console.log(scoreNotificationStart + userScore + scoreNotificationEnd)

```

，由於 JavaScript 有上述強制轉型的特性，你不需要做型別轉換就可以成功組合出結果：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4594/image_5.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4594/image_5.png)

這行程式碼沒有問題，不過有點太長了，而且你還要注意字母之間的空白。

# **方法二：Template Literals**

ES6 提供了更簡便的方法，叫做 template literals，它代表我們想要在字串裡放入特殊指令，有了 template literals 之後，你可以將上述程式碼改寫成：

```
let userScore = 10257
let scoreNotification = `Your score is: ${userScore} in this round.`
console.log(scoreNotification)

```

如你所見，你可以使用 `${}` 來嵌入變數，另外，你需要使用反引號 (`) 來宣告 template literal，也就是在 esc 下面的那個按鍵：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4595/image_6.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4595/image_6.png)

試著運行你的程式碼，然後看看結果如何。

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4596/image_7.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4596/image_7.png)

使用 template literals 讓程式碼更短、更易讀。任何用這種方式轉換的變數，都能順利被轉換成文字。這種作法大量運用在 HTML 文件裡，之後，當你開始組合 HTML 和 JavaScript 之後，你會發現它很好用！
