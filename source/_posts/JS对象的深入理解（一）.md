---
title: JavaScript对象的深入理解 （一）
date: 2017-9-19 17:07:59
tags: JavaScript
---

> 对象，一种数据类型。对象是**属性(变量)**和**方法(函数)**结合在一起的数据实体

对象的出现，就是为了解决**封装**的问题。可以将许多属性与方法封装在一个对象里，方便调用，也符合人的思考方式。

### JavaScript中创建对象的基本方法
1. 创建Object实例，再添加属性和方法
```
var person = new Object();
    person.name = "Jonathan";
    person.age = 23;
    person.job = "Developer";
    person.sayName = function () {
    console.log(this.name);
};
```

2. 对象字面量方法
由于上述写法繁琐，故出现了对象字面量方法创建对象。
```
var person = {
    name: "Jonathan",
    age: 23,
    job: "Developer",
    sayName: function () {
        console.log(this.name);
    }
};

console.log(person.name); //Jonathan
person.sayName(); //Jonathan
```
这样一来，就把属性和方法封装进了一个对象中，方便调用。

### 构造函数模式
如果要创建许多对象，传统方法存在以下问题
- 对象名太多，容易搞重复
- 新建一个对象就要全部重写属性和方法，过于复杂
- 无法发挥JavaScript的面向对象优势（继承）

由于JavaScript本身没有类的概念，因此诞生了构造函数模式来创建对象，该方法**利用函数创建对象**。由于函数本身也是对象，因此可以这么操作。
构造函数创建对象的方法是：
```
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function(){
                       console.log(this.name);
                   };    
}
        
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```
要点：
1. 构造函数命名应以**大写字母开头**（约定俗成的规矩）
2. 构造函数本身也是函数，只不过是用来创建对象的
3. 要创建对象的实例，必须要用**new**操作符，否则跟调用函数无异。
4. 任何函数，只要通过new操作符来调用，它就可以作为构造函数。

至此，一个Person对象的创建就完成了，它有以下优点：
- 新建对象只用给函数提供参数，简化了创建。
- 有了实例的概念，如Person1就是Person的实例。无形之中给对象归了类。
- 更好的体现了**封装**，创建对象只用给参数，不用关心对象内部细节。

**但**用构造函数模式的方法创建对象并不是完美的，它存在以下问题，即：
**每个方法（对象内置函数）都要在实例上重新创建一遍**
构造函数也可以用以下方法定义，方便我们发现问题

```
function Person(name, age, job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = new Function(console.log(this.name));
    };    
}
        
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");

console.log(person1.sayName == person2sayName); //false
```
在新建对象person1和person2时，分别新建了两个不同的方法person1.sayName()和person2.sayName()。
但这很没有必要，只需要公用一个sayName()方法就好了。为了解决上述问题，诞生了原型模式

