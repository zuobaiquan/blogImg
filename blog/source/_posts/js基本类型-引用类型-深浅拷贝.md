---
title: JS基本类型-引用类型-深浅拷贝
date: 2017-05-06 23:21:49
tags: JavaScript
---

在JavaScript中变量包含两种类型的值：一种是基本类型，一种是引用类型。
<!--more-->
	基本类型包括：数值、字符串、null、undefined、布尔值
	引用类型包括：对象、数组、函数、正则...
## 1.引用类型的动态属性

对于引用类型的值，我们可以为其添加属性和方法，也可以改变或删除属性和方法，

对于基本类型的值，尽管给其添加属性和方法不会报错，但这是无效的。

```javascript
var obj=new Object();
obj.name="zuobaiquan";
var str="zbq";
str.age=20;
console.log(obj.name);// zuobaiquan
console.log(str.age);// undefined
```

## **2.基本类型值和引用类型值的复制**

### 2.1基本类型值

基本类型值是指在栈内存保存的简单数据段，在复制基本类型值的时候，会开辟出一个新的内存空间，将值复制到新的内存空间。

```javascript
var a = 1;
var b = a;
a = 2;
console.log(a);//输出2；
console.log(b);//输出1；
```

var a = 1;

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506225039.bmp)

var b = a;

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506225115.bmp)

a = 2;



![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506225128.bmp)

从上面例子看出，当一个变量的值是基本类型，把它复制给另一个变量，复制完成后改变它的值，不会影响已经复制了它的值的变量。

### 2.1引用类型值

引用类型值是保存在堆内存中的对象，变量保存的只是指向该内存的地址，在复制引用类型值的时候，其实只复制了指向该内存的地址。

```javascript
var a = {
   name: 'Kitty',
   age: '20',
   sex: 'man'
};
var b = a;
a.name = 'Jack';
console.log(a);//输出{name: 'Jack',age: 20,sex: 'man'}
console.log(b);//输出{name: 'Jack',age: 20,sex: 'man'}
```

var a = {name: 'Kitty',age: '20',sex: 'man'};

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506225137.bmp)

var b = a;

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506225144.bmp)

a.name = 'Jack';

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506225153.bmp)

从上面例子看出，当一个变量的值是引用类型值，把它复制给另外一个变量，复制的只是指向储存对象内存的地址，所以复制完成后，改变它的值，会影响复制了它的值的变量。
**注意：**如果有两个变量的值是引用类型值，就算它们的值完全相同，它们也是不相等的，因为它们指向的内存地址不同，例子：

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506230932.bmp)

## 3.对象的浅拷贝和深拷贝

当一个变量是对象，如果像上面那样直接将一个变量赋值给另一个变量，如果改变某个变量的值，另外一个变量也会跟着改变，如果我们不想发生这种情况，就需要写一个函数用来拷贝对象。

### 3.1浅拷贝

当对象里的属性的值只有基本类型的值时候。

```javascript
var a = {
     name: 'Kitty',
     age: 12,
     sex: 'man'
}
function copy(obj){
    var newObj = {};
    for(vl in obj){
         newObj[vl] = obj[vl] 
    }
	return newObj;
}
```

例子：

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506231443.bmp)



从上面例子看到，我们通过这种方式拷贝对象，改变某个变量的值，并不会影响另一个变量。

### 3.1深拷贝

当对象里的属性的值还是一个对象，这时候用上面的方法就不行了，例子：

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506231645.bmp)

这时候要改进这个函数：

> 使用递归的方法：

```javascript
function deepCopy(obj){
     var newObj = {};
     for(vl in obj){
         if(typeof obj[vl] === 'object' && obj[vl] !== null){
             newObj[vl] = deepCopy(obj[vl]);
         }else{
             newObj[vl] = obj[vl];
         }       
     }
     return newObj;
}
```

例子：![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506231925.bmp)

> 使用JSON的方法：
>
> JSON.stringify()，将一个对象解析成字符串。
> JSON.parse()，从一个字符串中解析出json 对象。

我们可以使用上面两个个方法来进行对象的深拷贝：

```javascript
JSON.paese(JSON.stringify());
```

例子：

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170506232156.bmp)

参考：http://www.cnblogs.com/lijiayi/p/jsdeeepcopy.html