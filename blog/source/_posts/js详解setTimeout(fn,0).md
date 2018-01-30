---
title: js详解setTimeout(fn,0)
date: 2017-06-06 12:09:12
tags: JavaScript
---



来源：https://www.geekjc.com/post/58ca7d8d32129645947aec84

最近面试遇到一个题目,是有关setTimeout(fn,0)和闭包应用的,题目如下:

```javascript
for (var i = 0; i < 3; i++) {
    setTimeout(function() {
        console.log(i);
    }, 0);
    console.log(i);
}
```

我当时想都没想,直接给面试官说,输出0,1,2.结果可想而知^_^。<!--more-->

很多公司面试都爱出这道题，此题考察的知识点还是蛮多的。为了防止初学者栽在此问题上，此文稍微分析一下。都考察了那些知识点呢？异步、作用域、闭包，你没听错，是闭包。我们来简化此题：

```javascript
setTimeout(function() {
        console.log(1);
}, 0);
console.log(2);
```

先打印2，后打印1。因为是setTimeout是异步的。正确的理解setTimeout的方式(注册事件)：有两个参数，第一个参数是函数，第二参数是时间值。调用setTimeout时，把函数参数，放到事件队列中。等主程序运行完，再调用。没啥不好理解的。就像我们给按钮绑定事件一样：

```javascript
btn.onclick = function() {
   alert(1);
};
```

这么写完，会弹出1吗。不会！！只是绑定事件而已！必须等我们去触发事件，比如去点击这个按钮，才会弹出1。setTimeout也是这样的！只是绑定事件，等主程序运行完毕后，再去调用。setTimeout的时间值是怎么回事呢？比如：

```javascript
setTimeout(fn, 2000)
```

我们可以理解为2000之后，再放入事件队列中，如果此时队列为空，那么就直接调用fn。如果前面还有其他的事件，那就等待。因此setTimeout是一个约会从来都不准时的童鞋。继续看：

```javascript
setTimeout(function() {
   console.log(i);
}, 0);
var i = 1;
```

程序会不会报错？不会！而且还会准确得打印1。为什么？因为真正去执行console.log(i)这句代码时，var i = 1已经执行完毕了！所以我们进行dom操作。可以先绑定事件，然后再去写其他逻辑。

```javascript
window.onload = function() {
   fn();
}
var fn = function() {
   alert('hello')
};
```

这么写，完全是可以的。因为异步！

es5中是没有块级作用域的

```javascript
for (var i = 0; i < 3; i++) {}
console.log(i);
```

也就说i可以在for循环体外访问到。所以是没有块级作用域。但此问题在es6里终结了，因为es6，发明了let。

这回我们再来看看原题。原题使用了for循环。循环的本质是干嘛的？是为了方便我们程序员，少写重复代码。让我们倒退50年，原题等价于：

```javascript
var i = 0;
setTimeout(function() {
    console.log(i);
}, 0);
console.log(i);
i++;
setTimeout(function() {
    console.log(i);
}, 0);
console.log(i);
i++;
setTimeout(function() {
    console.log(i);
}, 0);
console.log(i);
i++;
```

因为setTimeout是注册事件。根据前面的讨论，可以都放在后面。原题又等价于如下的写法：

```javascript
var i = 0;
console.log(i);
i++;
console.log(i);
i++;
console.log(i);
i++;
setTimeout(function() {
    console.log(i);
}, 0);
setTimeout(function() {
    console.log(i);
}, 0);
setTimeout(function() {
    console.log(i);
}, 0);
```

这回你明白了为啥结果是0 1 2 3 3 3了吧。

那个，说它是闭包，又是怎么回事？为了很好的说明白这个事情，我们把它放到一个函数中：

```javascript
var fn = function() {
  for (var i = 0; i < 3; i++) {
  	setTimeout(function() {
  		console.log(i);
  	}, 0);
  	console.log(i);
  }
};
fn();
```

上面的函数跟我们常见另一个例子（div绑定事件）有什么区别：

```javascript
var fn = function() {
        var divs = document.querySelectorAll('div');
        for (var i = 0; i < 3; i++) {
                divs[i].onclick = function() {
                        alert(i);
                };
        }
};
fn();
```

点击每个div都会弹出3。道理是一样的。因为alert(i)中的i是fn作用越中的，因而这是闭包。《javascript忍者秘籍》书里把一个函数能调用全局变量，也称闭包。因为作者认为全局环境也可以想象成一个大的顶级函数。怎么保证能弹出0，1， 2呢。解决之道：以毒攻毒！再创建个闭包！！

```javascript
var fn = function() {
        var divs = document.querySelectorAll('div');
        for (var i = 0; i < 3; i++) {
                divs[i].onclick = (function(i) {
                        return function() {
                                alert(i);
                        };
                })(i);
        }
};
fn();
```

或者如下的写法：

```javascript
var fn = function() {
        var divs = document.querySelectorAll('div');
        for (var i = 0; i < 3; i++) {
                (function(i) {
                        divs[i].onclick = function() {
                                alert(i);
                        };
                })(i);
        }
};
fn();
```

因此原题如果也想setTimeout也弹出0，1，2的话，改成如下：

```javascript
for (var i = 0; i < 3; i++) {
    setTimeout((function(i) {
        return function() {
            console.log(i);
        };
    })(i), 0);
    console.log(i);
}
```

## 总结如下:

归根结底是要理解setTimeout(fn,0)的意思,是从下一个Event loop开始执行,即是等当前所有脚本执行完再运行,就是"尽可能早",还有就是闭包的运用。如果想深入理解的话,推荐篇文章,看完你就可以完全掌握这方面的知识点了:

1. [setTimeout(fn,0)](http://javascript.ruanyifeng.com/advanced/timer.html#toc4)

