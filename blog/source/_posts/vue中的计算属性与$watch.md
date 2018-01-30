---
title: Vue中的计算属性与$watch
date: 2017-04-29 23:11:49
tags: Vue
---

计算属性：在模板中绑定表达式是非常便利的，但是他们实际上只用于简单的操作。模板是为了描述视图的结构。在模板中放入太多的逻辑会让模板过重且难以维护。<!--more-->这就是为什么vue.js将绑定表达式限制为一个表达式。如果需要多于一个表达式的逻辑，应当使用计算属性。

```html
<div id="box">
    a={{a}},b={{b}}
</div>
```

```javascript
new Vue({
  data:{
    a:1
  },
  computed:{
    b:function(){
      return this.a + 1
    }
  }
}).$mount("#box");
```

这里我们声明了一个计算属性b。我们提供的函数将用作属性vm.b的getter

你可以打开浏览器的控制台，修改 vm。vm.b 的值始终取决于 vm.a 的值。

你可以像绑定普通属性一样在模板中绑定计算属性。Vue 知道  vm.b 依赖于vm.a，因此当vm.a 发生改变时，依赖于 vm.b 的绑定也会更新。而且最妙的是我们是声明式地创建这种依赖关系：计算属性的 getter 是干净无副作用的，因此也是易于[测试](http://lib.csdn.net/base/softwaretest)和理解的。

### 计算属性 vs. $watch

计算属性 vs. $watch

### 计算属性 vs. $watch

Vue.js 提供了一个方法 `$watch`，它用于观察 Vue 实例上的数据变动。当一些数据需要根据其它数据变化时， `$watch` 很诱人 —— 特别是如果你来自 Angularjs。不过，通常更好的办法是使用计算属性而不是一个命令式的 `$watch` 回调。考虑下面例子：

```html
<div id="box">
    {{fullName}}
</div>
```

```javascript
var vm=new Vue({
  el:"#box",
  data:{
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
});
//使用$watch
vm.$watch('firstName', function (val) {
  this.fullName = val + ' ' + this.lastName
})

vm.$watch('lastName', function (val) {
  this.fullName = this.firstName + ' ' + val
});
```

上面代码是命令式的重复的。跟计算属性对比：

```javascript

var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

这样更好，不是吗？

### 计算 setter

计算属性默认只是 getter，不过在需要时你也可以提供一个 setter：

```javascript

// ...
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
```

现在在调用 vm.fullName = 'John Doe' 时，setter 会被调用，vm.firstName 和vm.lastName 也会有相应更新。

关于计算属性背后的原理和技术细节详见[计算属性的奥秘](http://cn.vuejs.org/guide/reactivity.html#计算属性的奥秘)。

总结 ：

计算属性：用于简单场合，比如计算，合并字符串等；    

watch属性：用于耗时的，可以异步的获取远程服务上的数据这样的操作。

参考资料：

http://cn.vuejs.org/v2/guide/reactivity.html#main

http://cn.vuejs.org/v2/guide/computed.html

https://github.com/zuobaiquan/Vue/tree/master/01vue%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86

