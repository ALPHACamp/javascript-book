---
layout: default
title: 建構式的原型：Constrctor.prototype
parent: JavaScript 物件導向
nav_order: 2
permalink: constrctor-prototype.html
---
# 建構式的原型：Constrctor.prototype

上個單元中我們認識了原型和原型鏈的概念，在這個單元中，我們則要進一步把這些概念應用於 constructor function 裡。

我們會接續之前寫的 `AlphaPhone` 的建構式：

```jsx
// Constructor Function
function SmartPhone (name, price, features){
  // property
  this.name = name
  this.price = price
  this.features = features

  // method
  this.showPhoneInfo = function() {
    console.log(`The price of ${this.name} is $${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
  }
}
```

# 如果把方法寫在建構式函式中⋯⋯

之前我們提到「建議不要把方法寫在 constructor 裡」，到底這樣會發生什麼事呢？如果我們直接透過 `SmartPhone` 來產生物件：

```jsx
let alphaPhoneX = new SmartPhone('alphaPhoneX', 14999, ['long battery life', 'AI camera'])

let alphaPhoneY = new SmartPhone('alphaPhoneY', 18900, ['water proof', 'high screen resolution'])

let alphaPhoneZ = new SmartPhone('alphaPhoneZ', 23900, ['IP47', 'high screen resolution', 'full display'])
```

你會發現在每個物件裡面都包含了一個一模一樣的 `showPhoneInfo` 方法：

```jsx
// alphaPhoneX
SmartPhone {
  name: "alphaPhoneX",
  price: 14999,
  features: ["long battery life", "AI camera"],
  showPhoneInfo: function () { ... }
}

// alphaPhoneY
SmartPhone {
  name: "alphaPhoneY",
  price: 18900,
  features: ['water proof', 'high screen resolution'],
  showPhoneInfo: function () { ... }
}

// alphaPhoneZ
SmartPhone {
  name: "alphaPhoneZ",
  price: 23900,
  features: ['IP47', 'high screen resolution', 'full display'],
  showPhoneInfo: function () { ... }
}
```

這些物件存放於電腦的記憶體中，而之前我們提過物件是 share by reference 的，因此別忘了每個物件中的 `showPhoneInfo` 方法也會另外存放在記憶體裡，再用參照位址指回來。

所以這裡總共有三個 SmartPhone 實例物件、和三個物件中的 method，各自佔有獨立的記憶體空間。

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5235/ExportedContentImage_00.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5235/ExportedContentImage_00.png)

但顯然我們不需要 3 個 method。那麼在學過原型和原型鏈的概念後，我們可以怎麼樣做來避免這個問題呢？

# 將共用的方法放在原型中：Constructor.prototype

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5236/ExportedContentImage_01.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5236/ExportedContentImage_01.png)

之前提到，當我們呼叫某個物件的方法時，JavaScript 會透過原型鏈尋找該方法是否存在。也就是說，只需要把方法放進 constructor 的原型裡，每個物件實例就能呼叫到這個共享的方法。

# **定義 SmartPhone.prototype**

讓我們把建構式裡的 `showPhoneInfo()` 移到 `SmartPhone.prototype` 中：

```jsx
function SmartPhone (name, price, features){
  this.name = name
  this.price = price
  this.features = features
}

SmartPhone.prototype.showPhoneInfo = function() {
  console.log(`The price of ${this.name} is $${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
}
```

這麼做的話，會發生什麼事呢？

# **再次調用 showPhoneInfo**

讓我們再次透過 `SmartPhone` 來產生兩個物件實例：

```jsx
let alphaPhoneX = new SmartPhone('alphaPhoneX', 14999, ['long battery life', 'AI camera'])

let alphaPhoneY = new SmartPhone('alphaPhoneY', 18900, ['water proof', 'high screen resolution'])
```

接著我們分別呼叫 `showPhoneInfo`：

```jsx
alphaPhoneX.showPhoneInfo()
alphaPhoneY.showPhoneInfo()
```

它們一樣能成功呼叫 `showPhoneInfo()`，但是當我們用 `console.log()` 印出 `alphaPhoneX` 時，你不會再看到 `showPhoneInfo()`：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5237/ExportedContentImage_02.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5237/ExportedContentImage_02.png)

# **觀察 proto**

`showPhoneInfo` 到哪裡去了呢？如果把 `__proto__` 打開來看，你會發現 `showPhoneInfo` 跑到了原型裡：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5238/ExportedContentImage_03.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5238/ExportedContentImage_03.png)

這個 `.__proto__` 會指向 `SmartPhone.prototype`，使用同一個建構式產生的物件實例 (instance) 共享同一個原型，你可以用以下方式確認：

```jsx
alphaPhoneX.__proto__ === alphaPhoneY.__proto__    // true
```

使用同一個建構式產生的物件實例 (instance) 共享同一個原型。

(注意這裡的名稱很混淆，`__proto__` 是指向 `SmartPhone.prototype`，而 `.prototype` 是 constructor 定義原型的方法，在名稱上都稱作原型，不只是你，大家在溝通時常常會搞混，如果不清楚，隨時在 console 上實驗一下)

使用 `Object.getPrototypeOf(alphaPhoneX)` 來查看也會得到一樣的結果。

雖然 `showPhoneInfo` 方法沒有直接被放在物件裡，但透過原型鏈的運作，我們仍然能成功呼叫到它：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5239/ExportedContentImage_04.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5239/ExportedContentImage_04.png)

# alphaPhoneX.constructor

你會發現在 `alphaPhoneX.__proto__` 裡面還有一個 `__proto__` ，讓我們再打開來看看，你會發現一個名為 constructor 的屬性：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5240/ExportedContentImage_05.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5240/ExportedContentImage_05.png)

這個 `constructor` 指向 `SmartPhone` 建構式** (讓實例知道怎麼認祖歸宗) ：

```jsx
alphaPhoneX.constructor === SmartPhone   // true
```

或者，可以透過 `constructor.name` 這樣的方式來確認建構式的名稱：

```jsx
console.log(alphaPhoneZ.constructor.name)      // "SmartPhone"
```

# 動態修改 Prototype

現在你在 `SmartPhone.prototype` 裡定義好共用方法了，如果哪天想要修改原型裡的方法，你不需要回頭找到原始的程式碼再修改，只要再定義一次`SmartPhone.prototype.showPhoneInfo` 就可以了。

例如以下這一整段程式碼中，我們呼叫了兩次 `alphaPhoneX.showPhoneInfo()`：

```jsx
// Constructor Function
function SmartPhone (name, price, features){
  this.name = name
  this.price = price
  this.features = features
}

// Put methods in protoype
SmartPhone.prototype.showPhoneInfo = function() {
  console.log(`The price of ${this.name} is $${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
}

// create alphaPhoneX instance
let alphaPhoneX = new SmartPhone('alphaPhoneX', 14999, ['long battery life', 'AI camera'])

alphaPhoneX.showPhoneInfo()

// Modify showPhoneInfo in prototype
SmartPhone.prototype.showPhoneInfo = function() {
  console.log(`The phone '${this.name}' with the newest features such as ${this.features.join(', ')}, only cost $${this.price}`)
}

// same instance but with different result
alphaPhoneX.showPhoneInfo()
```

你會發現第二次呼叫內容，輸出的訊息已經被改變：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5241/ExportedContentImage_06.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5241/ExportedContentImage_06.png)

雖然我們在修改 `SmartPhone.prototype.showPhoneInfo` 這個方法之前就用 `new` 建立了 `alphaPhoneX` 實例，但是呼叫 `alphaPhoneX.showPhoneInfo()` 的時候，都會動態參照 `SmartPhoneInfo.protoype`，因此你一定會得到最新的 `showPhoneInfo` 的結果。

# Recap

相信看到這裡，這些新術語、新語法讓你有眼花繚亂的感受。其實沒那麼複雜，簡單來說就是：

- Constructor 裡放共享的屬性
- 共享的方法放進 Constructor.prototype
- 用 instance.constructor 可以找到原本的建構式
