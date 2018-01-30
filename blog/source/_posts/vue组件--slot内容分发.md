---
title: Vue组件--slot内容分发
date: 2017-04-30 21:11:49
tags: Vue
---

### **①概述：**

简单来说，假如父组件需要在子组件内放一些DOM，那么这些DOM是显示、不显示、在哪个地方显示、如何显示，就是slot分发负责的活。<!--more-->

### **②默认情况下**

父组件在子组件内套的内容，是不显示的。

例如代码：

```html
<div id="box">
    <aaa>
        <span>text是否显示</span>
    </aaa>
    <template id="tpl">
        <p>我是标签</p>
    </template>
</div>
<script>
    var vm = new Vue({
        el: '#box',
        components: {
            "aaa": {
                template: "#tpl"
            }
        }
    });
</script>
```

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170430202314.bmp)

显示内容是一个 p 标签 的内容，不包含span标签里面的内容；

### **③单个slot**

简单来说，只使用这个标签的话，可以将父组件放在子组件的内容，放到想让他显示的地方。

```html
<div id="box">
    <aaa>
        
    </aaa>
    <template id="tpl">
        <p>我是标签</p>
        <slot></slot>
    </template>
</div>
<script>
    var vm = new Vue({
        el: '#box',
        components: {
            "aaa": {
                template: "#tpl"
            }
        }
    });
</script>
```

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170430202324.bmp)

这样写的话，结果是：

```html
<p>我是标签</p>
<span>text是否显示</span>
```

即父组件放在子组件里的内容，插到了子组件的

```
<slot></slot>
```

位置；注意，即使有多个标签，会一起被插入，相当于用父组件放在子组件里的标签，替换了  slot  这个标签。

### **④具名slot**

将放在子组件里的不同html标签放在不同的位置

父组件在要分发的标签里添加 slot=”name名” 属性

子组件在对应分发的位置的slot标签里，添加name=”name名” 属性，

然后就会将对应的标签放在对应的位置了。

```html
<div id="box">
    <aaa>
        <span slot="second">56789</span>
        <span slot="first">12345</span>
    </aaa>
    <template id="tpl">
        <p>我是标签</p>
        <slot name='first'></slot>
        <slot name='second'></slot>
        <!--显示次序看模板-->
    </template>
</div>
<script>
    var vm = new Vue({
        el: '#box',
        components: {
            "aaa": {
                template: "#tpl"
            }
        }
    });
</script>
```

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170430202334.bmp)

```html
<p>我是标签</p>
<slot name='first'>12345</slot>
<slot name='second'>56789</slot>
```

### **⑤分发内容的作用域：**

被分发的内容的作用域，根据其所在模板决定，例如，以上标签，其在父组件的模板中（虽然其被子组件的children标签所包括，但由于他不在子组件的template属性中，因此不属于子组件），则受父组件所控制。

示例代码：

```html
<div id="box">
    <aaa>
        <span slot="second">56789</span>
        <span slot="first" @click="tobeknow">12345</span>
    </aaa>
    <template id="tpl">
        <p>我是标签</p>
        <slot name='first'></slot>
        <slot name='second'></slot>
        <!--显示次序看模板-->
    </template>
</div>
<script>
    var vm = new Vue({
        el: '#box',
        methods: {
            tobeknow: function () {
                alert(111111);
            }
        },
        components: {
            "aaa": {
                template: "#tpl"
            }
        }
    });
</script>
```

当点击文字12345的区域时（而不是按钮全部），会触发父组件的tobeknow方法。但是点击其他区域时则没有影响。

官方教程是这么说的：

> 父组件模板的内容在父组件作用域内编译；子组件模板的内容在子组件作用域内编译

### **⑥当没有分发内容时的提示：**

假如父组件没有在子组件中放置有标签，或者是父组件在子组件中放置标签，但有slot属性，而子组件中没有该slot属性的标签。那么，子组件的slot标签，将不会起到任何作用。除非，该slot标签内有内容，那么在无分发内容的时候，会显示该slot标签内的内容。

如示例代码：

```html
<div id="box">
    <aaa>
        <span slot="first">【12345】</span>
    </aaa>
    <template id="tpl">
        <div>
            <slot name='first'></slot>
            <p>我是标签1</p>
            <slot name='second'></slot>
            <p>我是标签2</p>
        </div>
    </template>
</div>
<script>
    var vm = new Vue({
        el: '#box',
        components: {
            "aaa": {
                template: "#tpl"
            }
        }
    });
</script>
```

![](http://files.cnblogs.com/files/zuobaiquan01/QQ%E6%88%AA%E5%9B%BE20170430205958.bmp)

说明：

【1】name=’first’的slot标签被父组件对应的标签所替换（slot标签内部的内容被舍弃）；

【2】name=’last’的slot标签，因为没有对应的内容，则显示该slot标签内部的内容。

### **⑦假如想控制子组件根标签的属性**

【1】首先，由于模板标签是属于父组件的，因此，将子组件的指令绑定在模板标签里，是不可以的（因为他归属于父组件）；

【2】假如需要通过父组件控制子组件是否显示（例如v-if或者v-show），那么这个指令显然是属于父组件的（例如放在父组件的data下面）。可以将标签写在子组件的模板上。

如代码：

```html
<div id="box">
    <button @click="abc=!abc">点击让子组件显示</button>
    <aaa v-if="abc">
    </aaa>
</div>
<script>
    var vm = new Vue({
        el: '#box',
        data: {
            'abc': false
        },
        components: {
            "aaa": {
                template: "<div>这里是子组件</div>"
            }
        },
    });
</script>
```

说明：通过父组件（点击按钮，切换v-if指令的值）控制子组件是否显示。

【3】假如需要通过子组件，控制子组件是否显示（比如让他隐藏），那么这个指令显然是属于子组件的（会将值放在子组件的data属性下），那么就不能像上面这么写，而是必须放置在子组件的根标签中。

```html
<div id="box">
    <button @click="toshow">点击让子组件显示</button>
    <aaa>
        <span slot="first">【12345】</span>
        <!--上面这行不会显示-->
    </aaa>
</div>
<script>
    var vm = new Vue({
        el: '#box',
        methods: {
            toshow: function () {
                this.$children[0].tohidden = true;
            }
        },
        components: {
            'aaa':{
                template: "<div v-if='tohidden' @click='tohide'>这里是子组件</div>",
                data: function () {
                    return {
                        tohidden: true
                    }
                },
                methods: {
                    tohide: function () {
                        this.tohidden = !this.tohidden;
                    }
                }
            }
        },
    });
</script>
```

说明：

点击子组件会让子组件消失；

点击父组件的按钮，通过更改子组件的tohidden属性，让子组件重新显示。

子组件的指令绑定在子组件的模板之中（如此才能调用）；

参考文章：

http://blog.csdn.net/sinat_17775997/article/details/52484072

https://github.com/zuobaiquan/Vue/blob/master/04vue%E7%BB%84%E4%BB%B6/vue%E7%BB%84%E4%BB%B6slot.html

https://github.com/zuobaiquan/Vue/blob/master/04vue%E7%BB%84%E4%BB%B6/vue%E7%BB%84%E4%BB%B6%E5%A4%9A%E4%B8%AAslot.html

