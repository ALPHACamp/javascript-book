---
layout: default
title: 原型繼承與原型鏈
parent: JavaScript 物件導向
nav_order: 3
permalink: prototype-prototype-chain.html
---
# 原型繼承與原型鏈

在這個單元裡，我們會來認識「原型繼承」的觀念，你會碰到一系列看似深奧的專有名詞，如「原型 (prototype) 」和「原型鏈 (prototype chain) 」，但別忘記，我們的目的是「讓一個物件取得另一個物件的屬性與方法」。

先定義一下「繼承 (inheritance)」和「原型繼承 (prototypal inheritance)」兩個術語：：

- 在 JavaScript 裡，「繼承」的定義是「讓一個物件取得另一個物件的屬性與方法」；
- JavaScript 的繼承系統會透過原型鍊 (prototype chain) 來連接到其他物件的功能，與「classical inheritance」的系統略有不同 (e.g. 沒有拷貝程式碼)，因此稱為「原型繼承」。

# 淺談 JavaScript 的原型繼𠄘

讓我們透過以下例子來展示「繼承」的概念，也就是「一個物件如何取得另一個物件的屬性與方法」。說明中會有一些陌生的術語，之後會慢慢介紹，請你先留意整體的觀念。

首先讓我們建立一個字串來當成例子：

```jsx
const name = 'AlphaPhoneX'
console.log(name)           // "AlphaPhoneX"
```

做為一個基本型別，`name` 本身並不具備屬性和方法，然而，字串 `name` 的原型來自建構子 String()，你可以用 `constructor.name` 來查看：

```jsx
const name = 'AlphaPhoneX'
console.log(name.constructor.name)          // "String"
```

我們確認了變數 `name` 是透過建構式函式 `String()` 產生的實例。此時，原型鏈可以呈現如下：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5225/ExportedContentImage_00.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5225/ExportedContentImage_00.png)

透過原型鏈，字串 `name` 可以取用 String.prototype 裡定義好的方法，因此你可以使用 `.split()`, `.slice()`, `.toLowerCase()` 等字串方法：

```jsx
name.toLowerCase()            // "alphaphonex"
name.slice(0, 5)              // "Alpha"
name.split('a')               // ["Alph", "PhoneX"]
```

這就是 JavaScript 裡的原型繼承，雖然有一些陌生的術語，但**核心目的是「取得另一個物件的屬性與方法」**，如此一來，你才能應用物件導向程式設計，把不同物件間共用的屬性與方法封裝到上層的範本裡。

# 什麼是原型？

每一個透過建構式函式產生的物件，都會攜帶一個原型物件，你可以把它想像成一個工具包，只要加入到這個工具包裡的屬性與方法，就能透過原型鏈來共享。

請在 console 裡使用 `name.` 時（打到 `.` 就好），這時候瀏覽器會很貼心的幫我們列出所有存在 `name` 本身的屬性或方法：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5226/ExportedContentImage_01.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5226/ExportedContentImage_01.png)

這裡看到的清單，是 `name` 的原型物件裡所有可用的屬性與方法，當你呼叫這些方法時，JavaScript 會透過原型鏈查找到可用的函式。

# 在原型鏈中尋找屬性與方法

接著讓我們看看呼叫方法時，實際的過程。例如當我們調用 `name.toLowerCase()` 時，JavaScript 會發生以下程式：

1. 查看 `name` 本身是否有 `toLowerCase` 方法，然後發現 `name` 沒有這個方法；
2. 到 「`name` 的原型」去找，也就是 String.protype，它會在這裡成功找到 `toLowerCase`。
3. 根據 String.prototype.toLowerCase 裡的函式設計，執行 `name.toLowerCase()`。

如果你調用一個不存在的方法如 `name.abc()`，它會一直向上找到 `null` 為止，才會確定 `name` 沒有這個方法而回傳以下錯誤：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5227/ExportedContentImage_02.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5227/ExportedContentImage_02.png)

# 查看原型鏈裡的資訊

# **查看某物件的原型：Object.getPrototypeOf()**

你可以使用 `Object.getPrototypeOf()` 來檢視某物件的原型：

```jsx
// Object.getPrototypeOf(name)
console.log(Object.getPrototypeOf(name))
```

從 `console` 的結果中可以發現 `name` 的原型是 `String`，也就是說，它產生自 constructor function `String`：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5228/ExportedContentImage_03.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5228/ExportedContentImage_03.png)

原型鏈可能不只一層，你可以進一步尋找 「name 的原型的原型」：

```jsx
let prototypeOfName = Object.getPrototypeOf(name)
let prototypeOfPrototypeOfName = Object.getPrototypeOf(prototypeOfName)
```

傳統上，另一種取得原型的方式是直接使用 `__proto__` 屬性，因此透過 `name.__proto__` 一樣可以取得 name 這個字串的原型，得到的結果會是一樣的：

```jsx
let prototypeOfName = name.__proto__
let prototypeOfPrototypeOfName = name.__proto__.__proto__
```

注意：雖然 `.__proto__` 看起來比較方便，我們在示範中也會使用，但這個方法已宣告未來可能會被棄用，因此在正式撰寫程式碼時，請使用 `Object.getPrototypeOf()` 來取得原型。

# 補充：在 JavaScript 中任何東西的原型最後都是來自物件

在瞭解了原型和原型鏈的概念後，是該來面對事實的時候了——**在 JavaScript 中幾乎所有資料型別的原型最後其實都是物件**。

聽到這你可能會有點訝異，之前不是還大費周章地介紹了 primitive type 和 object 的不同嗎？怎麼會說這些東西其實都來自物件呢？

注意，我們說的是「它們來自物件」，而不是「它們是物件」。

當我們知道如何使用 `Object.getPrototypeOf` 來檢視原型後，你可以試著觀察上面這些資料型態的原型，以數值 (Number) 為例：

```jsx
let number = 3
let prototypeOfNumber = Object.getPrototypeOf(number)
let prototypeOfPrototypeOfNumber = Object.getPrototypeOf(prototypeOfNumber)
let prototypeOfPrototypeOfPrototypeOfNumber = Object.getPrototypeOf(prototypeOfPrototypeOfNumber)
```

接著把它們 `console.log()` 出來看：

```jsx
console.log(prototypeOfNumber)                          // object created by Number()
console.log(prototypeOfPrototypeOfNumber)               // object created by Object()
console.log(prototypeOfPrototypeOfPrototypeOfNumber)    // null
```

你會發現 `number` 的原型是一個透過 `Number()` 建構式函式所建立的實例，裡面包含了許多給數值使用的方法，像是 `toExponential`, `toFixed` 等等：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5229/ExportedContentImage_04.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5229/ExportedContentImage_04.png)

我們還可以看到在 `prototypeOfNumber` 裡面還有 `__proto__` 這個屬性，意思就是說，`number` 的原型鏈不只一層，還有「`number` 的原型的原型」，一樣透過 `console` 出來可以看到：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5230/ExportedContentImage_05.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5230/ExportedContentImage_05.png)

你會發現，「number 的原型的原型」是透過 `Object()` 這個建構式函式所建立的實例，裡面有許多給物件可以使用的方法，像是 `hasOwnProperty()`, `isPrototypeOf()` 等等。

換句比較通俗的話來說，就是 `number` 的爸爸是 `Number()`，所以我們可以使用和數值有關的方法，而因為 `Number()` 的爸爸是 `Object()`，因此 `number` 除了具有數值相關的方法，但它同樣具有物件的方法在內可以使用。

從 `console.log()` 中我們也可以發現在 `prototypeOfPrototypeOfNumber` 沒有 `__proto__` 屬性了，表示這是最後一層的原型了。這也就是為什麼我們會說，**在 JavaScript 中幾乎所有的東西都是物件**，因為不論是字串、數值、布林值、陣列，甚至是函式，當我們使用 `Object.getPrototypeOf()` 去追尋它的祖宗時，你會發現都有物件的影子在內，而且也都可以使用物件的方法。

# Recap

在這個單元中提到了**原型 (prototype)** 和**原型鏈 (prototype chain)** 的概念，而且可以透過 `Object.getPrototypeOf()` 來知道在 JavaScript 中幾乎所有的東西都會繼承自物件，因此帶有可用的物件方法。在下個單元中，將進一步說明如何透過原型和原型鏈的概念，來把方法代入建構式函式中使用。
