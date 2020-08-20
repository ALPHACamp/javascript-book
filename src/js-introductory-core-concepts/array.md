---
layout: default
title: Array 陣列
parent: JavaScript 入門核心概念
nav_order: 4
permalink: array.html
---
# Array 陣列

資料其實有很多種型態，接下來要介紹的「陣列（array）」可以說是在 JavaScript 世界中處理資料時最常使用的資料格式。

因為在實務上，資料未必單獨出現，反而有很大的機會是同時出現一卡車的資料，這時，如何定義資料格式就是一門藝術了。

我們要介紹如何用陣列（array）與物件（object）來管理資料。先來認識這兩種資料結構的不同：

<table>
  {% for row in site.data.array.array %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>

在 JavaScript 裡，使用 index 的資料結構叫陣列，使用 key-value pair 的資料結構叫物件。在這個單元裡，我們會先介紹陣列，到下個單元再介紹物件。

陣列像是一個櫃子，有不同的抽屜讓我們存放資料。因此，陣列就是一組變數的集合，如同櫃子一般，每個抽屜都有不同且從 0 開始的編號，後面的櫃子緊接著前面的櫃子。

![https://assets-lighthouse.alphacamp.co/uploads/image/file/8669/ExportedContentImage_00.png](https://assets-lighthouse.alphacamp.co/uploads/image/file/8669/ExportedContentImage_00.png)

# 宣告陣列

在宣告陣列時，透過中括號 ``，將每個位置的內容物放入中括號 `` 內，並用逗號 `,` 隔開，而陣列內的內容可以是數值、字串或者另一個物件。

```
let myFriends = ['派大星', '章魚哥', '小蝸', '蟹老闆', '珊迪']
```

# 取出陣列的內容

你需要利用 index 來取出陣列的內容，取值的方式是在陣列名稱後加上中括號 `` 和索引數字。

### **用 push 增加陣列元素**

`.push()` 方法能把一個元素推送到陣列的尾端，例如：

```jsx
let myFriends = ['派大星', '章魚哥', '小蝸', '蟹老闆', '珊迪']myFriends.push('皮老闆')console.log(myFriends)

```

這個 `myFriends` 的陣列，就增加了 `皮老闆` 的名字：

![https://lh5.googleusercontent.com/WlVef7XTzQb428pMf4MfSf-gDbZaSR4hfOV_rbjYBzXVsKVKkDIRGaw-TuGiA7XQLADu6-0sfrCOVke2lGgo5S6iWIIvPAfUWkFHIiMbfNYi1n5wZSporfV54QxF1HDrAeim-Py4](https://lh5.googleusercontent.com/WlVef7XTzQb428pMf4MfSf-gDbZaSR4hfOV_rbjYBzXVsKVKkDIRGaw-TuGiA7XQLADu6-0sfrCOVke2lGgo5S6iWIIvPAfUWkFHIiMbfNYi1n5wZSporfV54QxF1HDrAeim-Py4)

如果想要一次增加兩個人，則需要寫成：

```jsx
let myFriends = ['派大星', '章魚哥', '小蝸', '蟹老闆', '珊迪']myFriends.push('皮老闆', '凱倫')console.log(myFriends)
```

請注意人名是字串，記得加上單引號：

![https://lh4.googleusercontent.com/sJ6XAcRa0AC1_ovLrJhynE0wPXdrdaOd-3bxfuArzJE_y6NnbM5l2dOHL6N-qlUYYL7-BonfQ0INiDi26mjyzBPU6oR_I7Tgi0TagJNcJM-FdNSlk28eXaWWJwa0cBvBZrMiwajW](https://lh4.googleusercontent.com/sJ6XAcRa0AC1_ovLrJhynE0wPXdrdaOd-3bxfuArzJE_y6NnbM5l2dOHL6N-qlUYYL7-BonfQ0INiDi26mjyzBPU6oR_I7Tgi0TagJNcJM-FdNSlk28eXaWWJwa0cBvBZrMiwajW)

### **用 concat 合併陣列**

你也可以使用 `.concat()` 方法，新開一個陣列，並與原始的陣列合併：

```jsx
let myFriends = ['派大星', '章魚哥', '小蝸', '蟹老闆', '珊迪']let myNewFriends = myFriends.concat(['皮老闆', '凱倫'])console.log(myNewFriends)
```

相對於 `.push()` 直接修改了 `myFriends` 這個陣列，注意這裡 `.concat()` 回傳了一個新陣列，我們運用等號把新陣列指派給另一個變數 `myNewFriends`。

仔細觀察下圖，`myFriends` 的內容並沒有改變：

![https://lh5.googleusercontent.com/waZUp1CG_hCWyTplZ0-ylWBCrz8s8S9CyZLshbGy5Tq1Obg_Jju_TcfS-8rj3ZWQDdUVguAaSWoUxs0J-fhKLCsTmfL6n4_RGsDIV5Gt6h6RSkmsbxh1e4krx_zdMzHkggLwIRnw](https://lh5.googleusercontent.com/waZUp1CG_hCWyTplZ0-ylWBCrz8s8S9CyZLshbGy5Tq1Obg_Jju_TcfS-8rj3ZWQDdUVguAaSWoUxs0J-fhKLCsTmfL6n4_RGsDIV5Gt6h6RSkmsbxh1e4krx_zdMzHkggLwIRnw)

### **用 pop 移除元素**

和 `.push()` 相反，如果你不小心錯誤新增了一個人（雖然其實全部都不是人）。可以使用 `.pop()` 來移除它：

```jsx
let myFriends = ['派大星', '章魚哥', '小蝸', '蟹老闆', '珊迪']myFriends.push('皮老闆')console.log(myFriends)myFriends.pop()console.log(myFriends)
```

`.pop()` 會直接移除陣列中的最後一個元素，你會得到：

![https://lh5.googleusercontent.com/_ErzX183FHweySB5N_Z9wOV5jm-w6va9a8awC2tsZlZGO-0bElihc5wZb4oc6OEhYOtsZSqG27n8i-AUp5Tcla2h_TrZTw-F08wezDq1HzePwwHvODu08Nw95LcsoOwy05VEpE22](https://lh5.googleusercontent.com/_ErzX183FHweySB5N_Z9wOV5jm-w6va9a8awC2tsZlZGO-0bElihc5wZb4oc6OEhYOtsZSqG27n8i-AUp5Tcla2h_TrZTw-F08wezDq1HzePwwHvODu08Nw95LcsoOwy05VEpE22)

### **常見陣列方法**

陣列可以用來做非常多的事情。上面是其中一些陣列方法的舉例，整理如下表。未來遇到需要使用的情景，或是想要查找新方法時，可以透過這個表格，找到適合搜尋的關鍵字：

<table>
  {% for row in site.data.array.array_methods %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>
