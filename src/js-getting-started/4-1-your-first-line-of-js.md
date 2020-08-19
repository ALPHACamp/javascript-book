# 寫下你的第一行 Javascript 程式碼：Repl.it

以傳統的開發流程而言，要怎麼開始「寫」程式呢？

在本地（也就是自己的電腦）中，我們會需要許多工具軟體，比如編輯器（editor）、編譯器（compiler）、連結器（linker）、除錯器（debugger）等，才能進行程式碼的撰寫、翻譯（將你寫的程式碼，翻譯成電腦看得懂的內容）、執行與偵錯。也會需要大量的資料夾，用來儲存不同內容的程式碼檔案、分類架構。

這些工具性軟體的集合，我們統稱為「開發環境」。

# 什麼是整合開發環境？

整合開發環境（Integrated Development Environment，簡稱 IDE，也有人稱為 Interactive Development Environment）指的其實就是一種程式開發的輔助軟體，集前述的工具軟體於一身，能讓使用者在一個集大成的開發環境下，使用友善的圖形介面進行撰寫、編譯、測試等。

你已經準備好學習第一個程式語言了。不過，要一一下載、安裝、設定這些工具，對於初學者而言太費力，因此，這裡向你介紹雲端的整合開發環境服務，如下圖的 Repl.it 與 CodePen 畫面：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8637/ExportedContentImage_00.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8637/ExportedContentImage_00.png)

直接在線上寫程式碼，免除了環境安裝的繁雜步驟，先專注於新語言的練習、熟悉，同時透過線上編輯器的即時預覽功能，讓我們更能觀察指令的變化。非常適合作為初學階段的工具夥伴！

# 註冊 Repl.it

請先到 [https://repl.it](https://repl.it/) 註冊。有了正式帳號以後，將能和其他人分享自己編寫的程式，其他人也能檢視你的程式碼、留下評語，或是將你的程式碼複製（fork）後，改寫成自己想要的版本。

# 建立一個新的 Repl.it

請找到選單列上的「+ new repl」按鈕，接下來會跳出視窗，讓你可以選擇程式語言，搜尋 JavaScript 之後，按下「Create repl」按鈕。

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8638/ExportedContentImage_01.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8638/ExportedContentImage_01.png)

接著你會看到下圖的畫面，我們會在畫面中間的白色區域編寫程式碼，寫完以後按下「run」，結果就會在黑色區域裡跑出來。

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8639/ExportedContentImage_02.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8639/ExportedContentImage_02.png)

如上圖所示，白色區域提供的是程式碼編輯器（editor）的功能；而黑色畫面則稱為 console。

Console 譯為「主控臺」，它的作用是讓開發人員能觀察系統的內部訊息，或者透過指令直接操作系統。我們可以在這裡即時測試 JavaScript 程式碼。

# 撰寫程式，輸出結果到 Console

請在編輯區域複製貼上這段程式碼：

```
console.log('Hello, World!')
```

然後按下上排綠色的「run」按鈕，你會在黑色區域裡，看到結果跑出來了：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/10400/ExportedContentImage_00.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/10400/ExportedContentImage_00.png)

你好，世界。

恭喜你！這是你寫下的第一行程式碼。

`console.log()` 是一個最基本的 JavaScript 函式，它可以將括號內的內容印出——意即在主控臺上顯示結果。