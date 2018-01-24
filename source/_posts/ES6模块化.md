---
title: ES6模块化| ES6学习
date: 2018-1-15 16:05:00
tags: JavaScript
---

####  模块的定义

> 模块是自动运行在严格模式下且没有办法退出运行的JS代码
>
> 模块与普通JS代码的区别在于**可定义导入导出绑定**



#### 导出

```javascript
// 导出数据
export var color = "red"
export let name = "Nicholas"
export const magicNumber = 7

// 导出函数
export function sum (num1, num2) {
	return num1 + num1
}

// 导出类
export class Rectangle {
	constructor (length, width) {
		this.Length = length
		this.Width = width
}

// 未导出则为模块私有
function subtract (num1, num2) {
	return num1 - num2
}

// 定义一个函数。...
function multiply (num1, num2) {
	return num1 * num2
}

// 导出引用
export { multiply }
```



#### 基本导入

```javascript
import { a, b } from 'example.js'
```



#### 整体导入

```javascript
import * as example from 'example.js'
```



#### 默认导入

```javascript
import sum from 'example.js'
```





