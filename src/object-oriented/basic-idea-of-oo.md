---
layout: default
title: 物件導向基本觀念 ｜ALPHA Camp
description: JavaScript 教學：物件導向基本觀念 
parent: JavaScript 物件導向
author: ALPHA Camp
nav_order: 1
permalink: basic-idea-of-oo.html
---
# 物件導向基本觀念

在這個章節，我們要來介紹物件導向程式設計 (Object-oriented programming)，物件導向程式設計可以幫助你更有效地管理程式碼。

讓我們舉個例子。假設我們有三支不同的手機，分別用變數 `alphaPhoneX`、`alphaPhoneY`、`alphaPhoneZ` 來表達：

![https://assets-lighthouse.alphacamp.co/uploads/image/file/5224/ExportedContentImage_00.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/5224/ExportedContentImage_00.png)

之前我們提到物件通常用來表達一組完整的概念，例如一支智慧型手機通常都會包含名稱、價格、特色等，按照過去的方法，我們可以直接用 object literal 建立物件：

```jsx
let alphaPhoneX = {
  name: 'AlphaPhoneX',
  price: 14999,
  features: ['long battery life', 'AI camera']
  showPhoneInfo: function () {
    console.log(`The price of ${this.name} is ${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
  }
}
```

當只有一支手機時，沒什麼問題。但如果你是一家手機設計公司，在公司的手機管理系統裡登錄了上百支不同的手機，每種手機的名稱、價格和特色都不太一樣，你會需要重覆建立物件，例如：

```jsx
let alphaPhoneX = {
  name: 'AlphaPhoneX',
  price: 14999,
  features: ['long battery life', 'AI camera']
  showPhoneInfo: function () {
    console.log(`The price of ${this.name} is ${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
  }
}

let alphaPhoneY = {
  name: 'AlphaPhoneY',
  price: 18900,
  features: ['water proof', 'high screen resolution']
  showPhoneInfo: function () {
    console.log(`The price of ${this.name} is ${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
  }
}

let alphaPhoneZ = {
  name: 'AlphaPhoneZ',
  price: 23900,
  features: ['IP47', 'high screen resolution', 'full display']
  showPhoneInfo: function () {
    console.log(`The price of ${this.name} is ${this.price}, which has the newest features such as ${this.features.join(', ')}.`)
  }
}
```

用這種方式重覆宣告新物件會有幾個壞處：1) 重複本身浪費時間；2) 光是 3 支手機就寫了一堆程式碼，難以想像有上百支手機時會需要維護多少程式碼；3) 無法確保每個人在宣告新物件時，都會用同樣的屬性名稱。

這時候我們會導入物件導向的概念，先統一為手機物件建立一個抽象化的簡單模型，然後在程式中使用此模型來快速建立結構一致的手機物件實例 (instance)。
