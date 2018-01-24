---
title: JSON初探
date: 2017-09-09 12:00:00
tags: JSON
---

JSON是什么？
> - JSON是一种**数据格式**，不是一种编程语言。
> - JSON**不属于Javascript**，尽管有相同的语法形式
> - 并不只是Javascript，很多语言都可以使用JSON交换数据

----------------

## JSON的语法
### JSON可以表示的值
1. 简单值
包括字符串、数值、布尔值、null
2. 对象
包括简单值或对象。为**不同类型的无序键值对集合**
3. 数组
包括简单值、对象、数组。为**相同类型的有序数据集合**

### JSON对象的构成方式
```
{
    "name":"Jonathan",
    "age":23,
    "job":"developer",
    "school": {
        "schName":"CDUT",
        "location": "Chenghua CD"
    }
}
```
要点：
1. 没有声明变量（不用在前面加var）
2. 没有末尾的分号
3. 对象的属性与属性名**必须加双引号**

### JSON数组的构成方式
```
[
  {
    "name": "John",
    "age": 24,
    "job": "writer"
  },
  {
    "name": "Bob",
    "age": 21,
    "job": "student"
  },
  {
    "name":"Jonathan",
    "age":23,
    "job":"developer",
    "school": {
        "schName":"CDUT",
        "location": "Chenghua CD"
    }
  }
]
```
要点：
1. 整个数组用[]包裹
2. 各元素用逗号,隔开
3. 对象表示法同上

