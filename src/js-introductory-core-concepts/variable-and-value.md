---
layout: default
title: Variable & Value 變數與值
parent: JavaScript 入門核心概念
nav_order: 1
permalink: variable-and-value
---
# Variable & Value 變數與值

# Variable & Value 變數與值

實際踏進了 JavaScript 語言的領域，接下來，你會透過幾個重要的元素，逐步認識它的基本語法。

首先從變數（variable）開始吧。

我們知道，我們是透過程式語言，來讓電腦操作資料。而在任何一個程式語言中，操作資料前，你會需要先找到一個地方放置這些資料。變數就是這樣的存在：它提供一個暫時儲存資料的地方，透過一個可以識別的名字，將資料寫進記憶體。

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8713/ExportedContentImage_00.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8713/ExportedContentImage_00.png)

如上圖，變數與資料操作的實際情況，在電腦上發生的是：

- 你在記憶體上宣告（declare）了一組變數
- 你在記憶體上創建（create）了一筆資料
- 變數指向（assign）這筆資料

當你要使用這筆資料進行運算時，便可以透過變數來操控。而其中需要特別留意的，就是給予變數一個有意義的名稱，提高程式碼可被閱讀、辨識的程度。

我們來看看 JavaScript 怎麼寫。以下列這行程式碼為例：

```
let myBirthday = '1986/07/14'
```

它的意思是，使用 `let` 的方式，宣告一個名為 `myBirthday` 的變數，並對應到一筆 ‘1986/07/14’ 的資料。

也就是說，當我們想要宣告一個變數時，我們會用像上述的句型。

在這行程式碼中，你可能注意到了一些有趣、很容易看懂的資訊，比如 `let` 這個詞、`myBirthday` 這個詞，以及 `=` 這個符號，讀起來似乎很接近一個簡化版、數學化的日常語句。

這個發現非常好，因為像 JavaScript 這樣的高階語言，本來就是為了讓人類讀懂而發明的，因此可讀性非常高。

以下，我們會依序講解上述句型中的：

- `let`
- `=`
- `myBirthday`

等單詞的用法與意義，它們分別代表的是對變數的宣告（declare）、指派（assign）與命名慣例（naming convention）等重要主題。

# 宣告

在 JavaScript 中，你需要運用特殊的關鍵字來宣告變數（可變動）與常數（不可變動），在本課程中採用 ES6 標準，因此，我們會使用 `let` 來宣告可變數，並使用 `const` 宣告常數：

當我們使用 `let` 關鍵字宣告變數時，代表我們預期資料是可以被改變的。開頭的例子中，我們用 `let` 宣告了變數 `myBirthday`，並存進一筆 `'1986/07/14'` 的生日資料。

我們在剛剛介紹的 [Repl.it](http://repl.it/) 網站中，開啟一個新的檔案實際嘗試一下。先在左邊的編輯器輸入：

```
let myBirthday = '1986/07/14';

```

可以使用 `console.log(myBirthday)` 看看結果：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8652/ExportedContentImage_01.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8652/ExportedContentImage_01.png)

接著，我們想要改寫資料的內容，因此我們在程式碼的第 3 行，重新指派 `myBirthday` 這個變數的內容，輸入：

```
myBirthday = '1978/01/02'

```

再次使用 `console.log`，將 `myBirthday` 印出到 console 裡。加上這段：

```
console.log('我的生日變成了', myBirthday)

```

你會發現，變數 `myBirthday` 裡的資料，已經改成了第 3 行重新指派的內容。從海綿寶寶的生日變成了派大星的生日（咦？）！

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8653/ExportedContentImage_02.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8653/ExportedContentImage_02.png)

這正是變數的有趣與重要之處。當今天是派大星的生日，你想要在派大星登入你的網站時，客製化一個特別的生日招呼訊息，就可以透過變數來呈現這個動態結果。

# **宣告常數**

與變數相反，當我們使用 `const` 來宣告時，我們預期這組資料不能被改變，也就是常數（constant）的概念。

我們用同樣的例子來試試看。將剛剛的程式碼第 1 行改成用 `const` 來宣告。此時當你執行程式碼，你會看到這個畫面：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8654/ExportedContentImage_03.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8654/ExportedContentImage_03.png)

右側的 console 顯示的仍然是第一組生日資料。往下則出現了一大段紅色的錯誤訊息。我們注意第一行：「TypeError: Assignment to constant variable.」

這句話描述了一個錯誤行為：對不變的變數（constant variable）指派新值。意思是，當使用 `const` 來宣告變數時，就無法在後續的程式碼裡修改這個變數裡的內容。

**Tips: 用新版的 let & const，不要用 var**

宣告變數時，記得使用 let 或 const。

雖然使用 var 乍看之下並沒有讓程式產生什麼問題，但使用 let 或 const 是目前業界的 best practice，建議養成習慣。

**Tips: let 和 const 該用哪一個？**

初學一門新工具時，這種「好像都可以、又好像需要想一下」的細膩抉擇最煎熬了！

由於 JavaScript 是一個很自由的語言，因此使用 const 可以避免宣告內容不要隨便被改動，在稍具規模且多人合作的專案，這是很重要的功能，像是商品價格、遊戲規則設計等等商業資訊，你絕對不會希望這些值被隨便改動——從「工程」的角度，沒有預設要變動的值，就需要確保它不能被變動，否則將導致混亂。

因此，在**實務上的原則是：除非有預期要改動，否則就用 const 宣告。**

# **賦值**

前面說過，變數與資料（物件）間是指派（assign）的關係。延續前面的例子，我們使用 `let` 關鍵字，宣告變數 ‘myBirthday’，並用 `=` 指派了資料到這個變數裡：

```
let myBirthday = '1986/07/14';

```

# **取值**

而 `console.log` 則是「取值」的意思，在主控臺中印出結果：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8655/ExportedContentImage_04.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8655/ExportedContentImage_04.png)

# 慣例

最後，你需要開始注意撰寫 JavaScript 的慣例。我們剛才練習了「宣告變數」的動作——這在不同程式語言中也許大同小異，但像是使用 `let/const` 宣告、使用 `=` 來為變數賦值等，這裡所使用的關鍵字或方法就會不盡相同。

# **命名**

在 JavaScript 中，為變數命名時，需注意以下幾點：

- 可以使用錢符（$）、底線（_）與數字進行命名。如 `$myBirthday `或` _myBirthday`（但以小寫英文字母開頭仍是最標準的做法）
- 可以使用英文大、小寫命名不同變數。如 `MyBirthday` 與 `myBirthday` 會被視作不同變數
- **數字不能作為變數開頭**。如 `myBirthday1`、`myBirthday_1` 或 `_myBirthday` 都沒問題，但 `1myBirthday` 就會產生錯誤。見下圖「Invalid or unexpected token」的錯誤訊息：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8657/ExportedContentImage_06.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8657/ExportedContentImage_06.png)

- 變數名稱是兩個單字以上的組合時，需採用駝峰命名法（camel case）。也就是將第一個單字之外的接下來每一個字首大寫，像你剛剛看到的 `myBirthday` 這樣的寫法。

請特別注意，CSS 的命名上，喜歡用 `my-Birthday` 這種寫法，稱為烤肉串命名法（kebab-case），這在 JavaScript 裡是不合法的方式。

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8658/ExportedContentImage_07.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8658/ExportedContentImage_07.png)
