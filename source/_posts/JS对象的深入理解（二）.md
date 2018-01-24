---
title: JavaScript对象的深入理解 （二）
date: 2017-11-2 17:17:00
tags: JavaScript
---

之前提到，构造函数方法创建对象存在着**方法不共享**的问题，因此引申出了原型模式创建对象

### 原型模式

>  原型模式旨在创建一个**模版对象**，该对象的**所有属性和方法**被其实例所共享。

#### 原型的概念

不同于构造函数模式创建对象只能单级即成，得益于**原型链**的概念，原型模式可实现类似其他OOP语言的多级继承。

> 原型链：一系列有**继承关系**的函数（对象）中[[prototype]]属性**自底向上**的指向

先给一个例子：

```javascript
function Person() {
    
}

Person.prototype = {
  	constructor: Person,
    name: "Jonathan",
    age: 23,
  	job: developer,
  	sayName: function() {
        console.log(this.name);
    }
}

person1 = new Person();
person2 = new Person();
```

该例子中各对象的关系如下

//

每一个函数（对象）都可以视为一个**模版**，向上看，该对象的[[prototype]]





#### 创建原型对象

```javascript
function Person() {
}

Person.prototype = {
  	constructor: Person,
    name: "Jonathan",
    age: 23,
  	job: developer,
  	sayName: function() {
        console.log(this.name);
    }
}

var person1 = new Person();
person1.sayName(); //"Jonathan"

var person2 = new Person();
person2.sayName(); //"Jonathan"

console.log(person1.sayName == person2.sayName); //true
```

要点

1. 先命名一个空函数
2. 用对象字面量方式，为该函数的.prototype属性添加原型属性及方法
3. 为了constructor属性的正确指向，应先把constructor指向该对象



#### 原型对象的问题

由于众多实例共享原型的属性，因此改变其中某个实例的属性会影响到全局，造成**属性污染**，例子如下：

```javascript
function Person(){
}

Person.prototype = {
    constructor: Person,
    name : "Nicholas",
    age : 29,
    job : "Software Engineer",
    friends : ["Shelby", "Court"],
    sayName : function () {
        alert(this.name);
    }
};

var person1 = new Person();
var person2 = new Person();

person1.friends.push("Van");

alert(person1.friends);    //"Shelby,Court,Van"
alert(person2.friends);    //"Shelby,Court,Van"
alert(person1.friends === person2.friends);  //true
```

可见，person1的friends属性污染了person2的friends属性。为避免这种情况，引入组合构造函数与原型模式。



### 组合使用构造函数与原型模式

单一使用原型对象的问题在于**所有属性皆共享**，若不想共享某属性，则可放入构造函数中。

```javascript
function Person(name, age, job){
   this.name = name;
    this.age = age;
    this.job = job;
    this.friends = ["Boy next door", "Deep dark fantasy"];
}

Person.prototype = {
    constructor: Person,
    sayName : function () {
        alert(this.name);
    }
};

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");

person1.friends.push("Van");

alert(person1.friends);    //"Shelby,Court,Van"
alert(person2.friends);    //"Shelby,Court"
alert(person1.friends === person2.friends);  //false
alert(person1.sayName === person2.sayName);  //true
```




