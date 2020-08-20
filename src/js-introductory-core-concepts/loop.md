---
layout: default
title: Loop 迴圈
parent: JavaScript 入門核心概念
nav_order: 7
permalink: loop.html
---
# Loop 迴圈

# Loop 迴圈

迴圈的用途是**重覆執行程式碼**，只要條件滿足，就會執行特定的動作。迴圈是程式能將人工流程自動化的關鍵工具。

初學階段，我們先來瞭解最基本的兩種迴圈：

- while：只要條件有效，就持續執行
- for：控制執行次數

# 只要條件有效，就持續執行：While 迴圈

一個典型的 while 迴圈如下：

```jsx
let x = 1
while (x <= 3) {
  console.log(`I have looped ${x} time(s)...`)
  x++
}
console.log('Finished!')

```

看看這程式碼，然後嘗試看看它會印出什麼來：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4608/image_1.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4608/image_1.png)

讓我們觀察一下 while 迴圈的語法結構：

- **關鍵字**：`while`；
- **條件**：在 `( )` 裡面定義條件，只要條件表達式 (expression) 回傳 true，就會執行 `{}` 裡的程序；
- **執行程序**：將你希望重複的動作定義在 `{ }`之中。

# **無限迴圈 (infinite loop)**

由於 while 迴圈依賴條件式運行，只要條件有效，就會持續執行，所以要小心寫出無限循環的迴圈。例如：

```
while (true) {
  console.log('This loop is running.....')
}
```

在你試著去執行以上程式之前，先提醒你，如果你寫出了這樣的迴圈，因為程式無窮循環，會讓瀏覽器進入接近當機狀態，同時你會看見 console 持續輸出訊息：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4609/image_2.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4609/image_2.png)

你會需要把瀏覽器關掉，才能跳脫這個窘境。體驗過這種當機之後，你應該能體會為什麼我們要說「小心無限迴圈」了吧！

# 控制執行次數：for 迴圈

不同於 while 迴圈以條件是否為 true 為旗標，for 迴圈會指定明確的執行次數，例如：

```
for (let x = 1; x <= 3; x++ ) {
    console.log(`I have looped ${x} time(s)...`)
}
console.log('Finished!')
```

執行起來是這樣：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4610/image_3.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4610/image_3.png)

讓我們觀察一下 for 迴圈的語法結構：

- **關鍵字**：`for`；
- **條件**：在 `( )` 裡面需要定義三種資訊：

1. 宣告索引變數，請注意需要關鍵字如 `let x = 1`；

2. 停止條件，如 `x <= 3`，在此條件為 true 之前，迴圈都會執行；

3. 每次迭代的變化，如 `x++` 讓迴圈每執行一次，做為索引的變數 `x` 就會加 1。

- **執行程序**：將你希望重複的動作定義在 `{ }`之中。

# **For 迴圈與陣列**

陣列常常會和 for 迴圈搭配使用，讓我們來練習看看。

以下的陣列是冰島語對星期一到日的稱呼，我們使用 `const` 宣告 `weekDays` 來存放陣列，因為這組資料應該不會改變。

```
const weekDays = ['Mánudagur', 'Þriðjudagur', 'Miðvikudagur', 'Fimmtudagur', 'Föstudagur', 'Laugardagur', 'Sunnudagur' ]
```

現在，我們想要按照順序印出一星期的天數。我們可以藉由以下的笨方法來慢慢寫：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4611/image_4.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4611/image_4.png)

如果我想要用 for 迴圈來印出星期一到日，請問要怎麼得知陣列的長度呢？

你可以使用 `weekDays.length` 來計算陣列長度。因此，就可以寫出以下程式碼：

```
for (let x = 0; x < weekDays.length; x++) {
  console.log(weekDays[x])
}
```

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4614/image3.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4614/image3.png)

如果我們想把星期的順序顛倒過來，可以改成這樣：

```jsx
for (let x = weekDays.length - 1; x >= 0 ; x--) {
  console.log(`${weekDays[x]} is day ${x + 1}`)
}
```

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4613/image2.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4613/image2.png)

# 跳脫迴圈：break

偶爾會遇到需要強制脫離迴圈的情境，這時候可以使用 `break`。例如這邊有一份食材清單，你要寫出一支程式來印出這份食材清單：

```
let items = ['lemons','bananas','stem ginger','<malicious code>','cocoa nibs']

let items = ['lemons','bananas','stem ginger','<malicious code>','cocoa nibs']
for (i = 0; i < items.length; i++) {
    console.log(items[i])
}
```

然而，有一組「惡意程式碼 ( `<malicious code>`)」隱藏在清單中。如果迭代到這組惡意程式碼，你需要中斷迴圈，避開危險。

要做到這個功能，我們需要做到以下事情：

- 用 `"<"` 當成檢查的目標，如果 `"<"` 存在，就表示遇到惡意的內容，我們會使用`_string_.indexOf(_string_)` 方法，它會在一個字串中搜尋另一個字串，如果它沒找到相對應的字串，會回傳 -1；
- 跳出迴圈，使用 **break**。

改寫之後的程式如下：

```
const items = ['lemons','bananas','stem ginger','<malicious code>','cocoa nibs']
let count = 0;
for (i = 0; i < items.length; i++) {
  if (items[i].indexOf('<') >= 0) break
  console.log(items[i])
  count++
}
console.log(`There are ${items.length} items in the list. The app accepted ${count} of them. `)
```

注意我們這次沒有使用 `{}`，這是因為如果條件為真，需要執行的動作只有 `break`，當程式碼只有一行時，可以接在 `if (condition)` 之後，程式仍然可以判斷。

這樣的寫法可以增加程式碼的可讀性，提升程式碼的可維護性。（注意，我們的重點是可讀性，而不是寫愈短愈厲害）。

然而，如果程式碼超過一行以上，你需要使用 `{}` 來宣告 code block。

試著執行看看：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/4612/image_5.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/4612/image_5.png)

只要 `.indexOf()` 指令找到 "<"，它就會中斷迴圈，但迴圈之外的程式仍然會繼續執行，因此 `console.log` 還是會印出訊息。請注意 `count` 數到 3 就停止了。
