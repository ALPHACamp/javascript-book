---
layout: default
title: Operator 運算子 - JavaScript 教學｜ALPHA Camp
parent: JavaScript 入門核心概念
image: https://assets-lighthouse.alphacamp.co/uploads/image/file/14034/operator.jpg
author: ALPHA Camp
nav_order: 3
permalink: operator.html
---
# Operator 運算子

運算子 (operator) 可以對 value 做處理，並且回傳新的 value，我們將會介紹以下運算子：

- 算術運算子（arithmetic operators）
- 賦值運算子（assignment operators）
- 比較運算子（comparison operators）
- 邏輯運算子 （logical operators）

## 算術運算子 (arithmetic operators)

最基本的是數學四則運算的符號，讓你可以對兩組 value 進行加減乘除：

<table>
  {% for row in site.data.operator.arithmetic %}
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

此外還有比較特別的：

<table>
  {% for row in site.data.operator.more_operators %}
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

## 賦值運算子 (assignment operators)

目前為止我們一直使用的 `=`，是一種賦值運算子，除此之外還有：

<table>
  {% for row in site.data.operator.assignment %}
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

## 比較運算子 (comparison operators)

比較運算子陳述的是邏輯關係，他會對前後的 value 進行比較，然後回傳 boolean 值，也就是 `true` 或是 `false`。

<table>
  {% for row in site.data.operator.comparison %}
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

## **邏輯運算子**

<table>
  {% for row in site.data.operator.logical %}
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
