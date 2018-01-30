---
title: js中的arguments用法
date: 2017-07-16 21:21:02
tags: JavaScript
---



```javascript
//arguments对象并不是一个数组，但是访问单个参数的方式与访问数组元素的方式相同
function show(){
    console.log(arguments); 
    //arguments.push(5);   //此时报错arguments.push is not a function
}
show(1,2,3,4);
//在js中 不需要明确指出参数名，就能访问它们，例如：

function test() {
    var s = "";
    for (var i = 0; i < arguments.length; i++) {
        alert(arguments[i]);
    }
}
test("name", "age");
//arguments.callee引用函数自身。
//callee 属性是 arguments 对象的一个成员，仅当相关函数正在执行时才可用。
//callee 属性的初始值就是正被执行的 Function 对象，这允许匿名的递归函数。
var sum = function (n) {
    if (n==1) {
        return 1;
    }else {
        return n + arguments.callee(n - 1);
    }
}
alert(sum(6));
//总结：arguments此对象大多用来针对同个方法多处调用并且传递参数个数不一样时进行使用。
//根据arguments的索引来判断执行的方法。
```