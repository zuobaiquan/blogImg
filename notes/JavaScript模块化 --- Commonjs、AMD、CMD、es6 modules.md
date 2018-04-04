# Commonjs、AMD、CMD、es6 modules的发展阶段

随着前端js代码复杂度的提高，JavaScript模块化这个概念便被提出来，前端社区也不断地实现前端模块化，直到es6对其进行了规范，下面就介绍JavaScript模块化。 

这篇文章还是希望能给大家一个比较好的思路，即JavaScript模块化是如何一步一步地发展起来的，
并且也会主要对这些模块化方式做一个简单的比较。

## 第一阶段：无模块化

　　JavaScript最初的作用仅仅是验证表单，后来会添加一些动画，但是这些js代码很多在一个文件
中就可以完成了，所以，我们只需要在html文件中添加一个script标签。 

　　后来，随着前端复杂度提高，为了能够提高项目代码的可读性、可扩展性等，我们的js文件逐渐
多了起来，不再是一个js文件就可以解决的了，而是把每一个js文件当做一个模块。
那么，这时的js引入方式是怎样的呢？大概是下面这样：

        ```
       <script src="jquery.js"></script>
　　<script src="jquery_scroller.js"></script>
　　<script src="main.js"></script>
　　<script src="list.js"></script>
　　<script src="detail.js"></script> 
   ```
     即简单的将所有的js文件统统放在一起。但是这些文件的顺序还不能出错，
比如jquery需要先引入，才能引入jquery插件，才能在其他的文件中使用jquery。 

**优点：**
     相比于使用一个js文件，这种多个js文件实现最简单的模块化的思想是进步的。　

**缺点：** 
    污染全局作用域。 因为每一个模块都是暴露在全局的，简单的使用，会导致全局变量命名冲突，
当然，我们也可以使用命名空间的方式来解决。

     对于大型项目，各种js很多，开发人员必须手动解决模块和代码库的依赖关系，后期维护成本较高。
依赖关系不明显，不利于维护。 比如main.js需要使用jquery，但是，从上面的文件中，我们是看不出来的，如果jquery忘记了，那么就会报错。 

## 第二阶段： CommonJS规范

　　CommonJS就是一个JavaScript模块化的规范，该规范最初是用在服务器端的node的，前端的webpack也是对CommonJS原生支持的。 

　　根据这个规范，每一个文件就是一个模块，其内部定义的变量是属于这个模块的，不会对外暴露，
也就是说不会污染全局变量。 

　　CommonJS的核心思想就是通过 require 方法来同步加载所要依赖的其他模块，然后通过 exports 
或者 module.exports 来导出需要暴露的接口。如下所示：

```
// a.js
var x = 5;
var addX = function (value) {
  return value + x;
};
module.exports.x = x;
module.exports.addX = addX;
```
这里的a.js就是一个CommonJS规范的模块了。 这里的module就代表了这个模块，module的exports属性就是对外暴露的接口，可以对外导出外部可以访问的变量，比如这里的x和addX。 

>exports 是对 module.exports 的引用。比如我们可以认为在一个模块的顶部有这句代码：
` exports = module.exports`
所以，我们不能直接给exports赋值，比如number、function等。  

  **注意：** 
因为module.exports本身就是一个对象，所以，我们在导出时可以使用 
`module.exports = {foo: 'bar'} `
也可以使用 
`module.exports.foo = 'bar'`
但是, exports 是 module.exports 的一个引用，或者理解为exports是一个指针，
exports指向module.exports，这样，我们就只能使用 exports.foo = 'bar' 的方式，
而不能使用 `exports = {foo: 'bar'}` 这种方式，
因为 `exports = {foo: 'bar'}` 这种方式的使用就会导致exports指向了别的对象，
那么这个模块的输出就会有问题了。

然后我们就可以在其他模块中引入这个模块使用了：

```
vara = require('./a.js');
console.log(example.x); // 5
console.log(example.addX(1)); // 6
```
　这里的require就会获取到a.js所暴露的module.exports变量，然后就可以使用其暴露的x和addX了。 

**优点：**
　　CommonJS规范在服务器端率先完成了JavaScript的模块化，解决了依赖、全局变量污染的问题，这也是js运行在服务器端的必要条件。

**缺点：**
　　这篇文章我们讲的主要是浏览器端js的模块化， 由于 CommonJS 是同步加载模块的，在服务器端，文件都是保存在硬盘上，所以同步加载没有问题，但是对于浏览器端，需要将文件从服务器端请求过来，那么同步加载就不适用了，所以，CommonJS是不适用于浏览器端的。 

## 第三阶段： AMD规范

　　之前提到: CommonJS规范加载模块是同步的，也就是说，只有加载完成，才能执行后面的操作。AMD规范则是非同步加载模块，允许指定回调函数。由于Node.js主要用于服务器编程，
模块文件一般都已经存在于本地硬盘，所以加载起来比较快，不用考虑非同步加载的方式，
所以CommonJS规范比较适用。但是，如果是浏览器环境，要从服务器端加载模块，
这时就必须采用非同步模式，因此浏览器端一般采用AMD规范。
而AMD规范的实现，就是大名鼎鼎的require.js了。 

> AMD标准中，定义了下面两个API：
> 1. require([module], callback)
> 2. define(id, [depends], callback)

　　即通过define来定义一个模块，然后使用require来加载一个模块。 
并且，require还支持CommonJS的模块导出方式。 定义alert模块：

```
define(function () {
    var alertName = function (str) {
      alert("I am " + str);
    }
    var alertAge = function (num) {
      alert("I am " + num + " years old");
    }
    return {
      alertName: alertName,
      alertAge: alertAge
    };
  });
```

引入模块：

```
require(['alert'], function (alert) {
  alert.alertName('JohnZhu');
  alert.alertAge(21);
});
```
但是，在使用require.js的时候，我们必须要提前加载所有的依赖，然后才可以使用，
而不是需要使用时再加载。

**优点：**
适合在浏览器环境中异步加载模块。
可以并行加载多个模块。

**缺点：**
 提高了开发成本，并且不能按需加载，而是必须提前加载所有的依赖。 

## 第四阶段：CMD规范

    CMD规范是阿里的玉伯提出来的，实现js库为sea.js。 它和requirejs非常类似，
即一个js文件就是一个模块，但是CMD的加载方式更加优秀，是通过按需加载的方式，
而不是必须在模块开始就加载所有的依赖。如下：

```
define(function(require, exports, module) {
  var $ = require('jquery');
  var Spinning = require('./spinning');
  exports.doSomething = ...
  module.exports = ...
})
```

**优点：**
1. 同样实现了浏览器端的模块化加载。
2. 可以按需加载，依赖就近。 

**缺点：**
　　依赖SPM打包，模块的加载逻辑偏重。 

    其实，这时我们就可以看出AMD和CMD的区别了，前者是对于依赖的模块提前执行，而后者是延迟执行。 前者推崇依赖前置，而后者推崇依赖就近，即只在需要用到某个模块的时候再require。 如下：

```
// AMD
define(['./a', './b'], function(a, b) {  // 依赖必须一开始就写好  
   a.doSomething()    
   // 此处略去 100 行    
   b.doSomething()    
   ...
});

// CMD
define(function(require, exports, module) {
   var a = require('./a')   
   a.doSomething()   
   // 此处略去 100 行   
   var b = require('./b') 
   // 依赖可以就近书写   
   b.doSomething()
   // ... 
});
```
## 第五阶段： ES6模块化

　　之前的几种模块化方案都是前端社区自己实现的，只是得到了大家的认可和广泛使用，而ES6的模块化方案是真正的规范。 在ES6中，我们可以使用 import 关键字引入模块，通过 exprot 关键字导出模块，功能较之于前几个方案更为强大，也是我们所推崇的，但是由于ES6目前无法在浏览器中执行，所以，
我们只能通过babel将不被支持的import编译为当前受到广泛支持的 require。 
　　虽然目前import和require的区别不大，但是还是推荐使用使用es6，因为未来es6必定是主流，对于代码的迁移成本还是非常容易的。  如：

```
  import store from '../store/index'
  import {mapState, mapMutations, mapActions} from 'vuex'
  import axios from '../assets/js/request'
  import util from '../utils/js/util.js'

  export default {
    created () {
      this.getClassify();  
      this.RESET_VALUE();
      console.log('created' ,new Date().getTime()); 
    }
```
