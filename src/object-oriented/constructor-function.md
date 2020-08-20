---
layout: default
title: 建構物件範本：Constructor Function
parent: JavaScript 物件導向
nav_order: 4
permalink: constructor-function.html
---
# 建構物件範本：Constructor Function

我們可以使用建構式函式 (constructor function) 來快速產生許多相同屬性或方法的物件。

# 什麼是 Constructor Function？

你可以把建構式函式 (constructor function) 想像成「餅乾壓模器」，若在製作餅乾的過程中使用「壓模機」，就可以快速做出形狀類以的餅乾。同理，constructor function 可以快速地產生結構相似的物件。

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5231/ExportedContentImage_00.jpg](https://assets-lighthouse.alphacamp.co/uploads/image/file/5231/ExportedContentImage_00.jpg)

從名字來看，constructor function 是一個 function，他的基本語法和平常寫 function 差不多；而 constructor 這個字可譯為「建構式」或「建構子」，在物件導向程式設計裡，用來創造物件的工具通常被稱為 constructor。

因此，constructor function 就是用來創造物件的函式，下文有時會簡稱 constructor。

# 用 Constructor Function 創造物件

# **定義 Constructor Function**

現在讓我們用 constructor function 來建立一個手機範本：

```jsx
// Define a constructor function
function SmartPhone (name, price, features) {
  this.name = name
  this.price = price
  this.features = features
  this.showPhoneInfo = function () {
    console.log(`The price of ${this.name} is ${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
  }
}
```

和一般使用 function 不同的地方是：

- 函式名稱使用大寫，以方便一看就知道這個函式是個 constructor。(使用小寫不會出錯，但不符合慣例)
- 建構式函式不能用 `return` 指定要回傳其他內容，如果加上 `return`，就只會回傳指定內容，而不會回傳一個新物件。

# **new**

接著讓我們運用定義好的 `SmartPhone` 函式來建立物件，請在呼叫函式時加上 `new`：

```jsx
// use 'new keyword to create object instance
let alphaPhoneX = new SmartPhone('alphaPhoneX', 14999, ['long battery life', 'AI camera'])

let alphaPhoneY = new SmartPhone('alphaPhoneY', 18900, ['water proof', 'high screen resolution'])

let alphaPhoneZ = new SmartPhone('alphaPhoneZ', 23900, ['IP47', 'high screen resolution', 'full display'])
```

這樣一來就快速建立了三個物件！

由於 constructor 裡定義的物件範本是抽象的手機，而物件實例是具體的手機，為了區分，由建構式 (constructor) 建立的物件會被稱為「**實例 (instance)**」；在這裡，`alphaPhoneX`, `alphaPhoneY`, `alphaPhoneZ` 都是由 `SmartPhone` 建立的**實例 (instance)** 。

# 觀察 Console 裡的資訊

讓我們用 `console.log(alphaPhoneX)` 來觀察看看 console 裡的訊息：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5232/ExportedContentImage_01.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5232/ExportedContentImage_01.png)

我們可以看到，`alphaPhoneX` 物件具備了建構式 `SmartPhone` 裡設定的屬性 `name`, `price`, `features` 與方法 `showPhoneInfo`。

注意，和單純透過 object literal 建立的物件相比，在大括號 `{ }` 前面會列出這個物件是透過哪個 constructor function：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5233/ExportedContentImage_02.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5233/ExportedContentImage_02.png)

你可以使用 `constructor.name` 的方式取得該建構式函式的名稱：

```jsx
console.log(alphaPhoneX.constructor.name)        // 'SmartPhone'
```

# 關鍵字 new 到底做了什麼事？

瞭解了建構式函式的用法之後，讓我們回頭來看一下過程中發生了什麼事？以這段程式碼為例，在呼叫建構式函式 `SmartPhone()` 之前，我們使用了 `new` 這個關鍵字：

```jsx
let alphaPhoneX = new SmartPhone('alphaPhoneX', 14999, ['long battery life', 'AI camera'])
```

**當我們使用 `new` 這個關鍵字時，會按順序發生以下的事情：**

1. 先有一個空物件被建立，
2. 執行 `SmartPhone` 函式；
3. `SmartPhone` 裡的 `this` 被指定成剛剛的空物件。

所以，執行到 `SmartPhone()` 裡的 `this.name`, `this.price` 和 `this.features` 時，**因為 `this` 指稱的是那個空物件，所以參數傳入的屬性和方法，就會被放進這個空物件**。

若要更清楚的看到這個過程，你可以在 constructor 裡加入 `console.log(this)` 來觀察：

```jsx
function SmartPhone(name, price, features){
  console.log(this)

  this.name = name
  console.log(this)

  this.price = price
  console.log(this)

  this.features = features
  console.log(this)

  this.showPhoneInfo = function() {
    console.log(`The price of ${this.name} is ${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
  }
  console.log(this)
}

let alphaPhoneX = new SmartPhone('alphaPhoneX', 14999, ['long battery life', 'AI camera'])
```

結果會像這樣：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5234/ExportedContentImage_03.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5234/ExportedContentImage_03.png)

就如先前提到的，它會先產生一個空物件 `{ }` ，而 `this` 會指稱到這個空物件，於是再把屬性 `name`, `price`, `features` 一個一個放進去。在建構式函式中所放入的方法 (`this.showPhoneInfo`) 也是一樣的意思。

前面提過，在使用 constructor function 的時候是不寫 `return` 的，所以請注意，若忘記加上 `new` 關鍵字，就會變成單純呼叫函式，而回傳 `undefined`：

```jsx
let alphaPhoneX = SmartPhone('alphaPhoneX', 14999, ['long battery life', 'AI camera'])
```

因此，大寫開頭的命名，可以幫助我們區分在呼叫 constructor function 時，前面理應加上 `new` 關鍵字。

# 盡可能不要把方法寫在建構式函式中

在上面的例子中，為了方便展示，我們直接把方法 `this.showPhoneInfo` 寫在建構式函式中，但一般來說，我們不會這樣做，因為每次當你 new 一個新物件時，物件裡都會攜帶一個新的 function，這個 function 會佔用新的記憶體空間，但明明都是在做一樣的事。

因此，我們會傾向把方法放進物件原型 (prototype) 並運用原型鏈 (prototype chain) 來使用物件
