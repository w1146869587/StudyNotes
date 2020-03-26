# vue笔记

## 一、起步

 var vm = new Vue({

​        el:'#vue_det',

​		 data:{

​			site:'菜鸟教程'，

​		}，

​		methods:{

​			details:function(){

​					return this.site + "-学的不仅是技术，更是梦想-";

​			 }

​		}

})

## 二、模板语法

vue.js使用了基于HTML的模版语法，允许开发者声明式地将DOM绑定至底导Vue实例的数据。

Vue.js的核心是一个充许你采用简洁的模板语法来声明式的将数据渲染进DOM的系统。

结合响应系统，在应用状态改变时，Vue能够智能地计算出重新渲染组件的最小代价并应用到DOM操作上。

 ![2018101212522327](D:\myNotes\StudyNotes\vue\vue笔记.assets\2018101212522327.png)

### 1、插值[{{}}]

{{}}

### 2、Html[v-html]

使用 v-html指令用于输出html代码： 

```html
<div id="app">
    <div v-html="message"></div>
</div>
    
<script>
new Vue({
  el: '#app',
  data: {
    message: '<h1>菜鸟教程</h1>'
  }
})
</script>
```

### 3、属性[v-bind]

HTML属性中的值应用v-bind指令,绑定属性

v-bind绑定属性样式---class的三种绑定方式

1）、布尔值的绑定方式

```html
<div id="demo">
　　<span v-bind:class="{‘class-a‘:isA ,‘class-b‘:isB}"></span>
</div>

var vm = new Vue({
　　　　el:"#demo",
　　　　data:{
　　　　　　isA: true,
　　　　　　isB: true
　　　　}
})
```

2）、变量的绑定方式

```html
<div id="demo">
<span :class=[classA,classB]></span>
</div>

var vm = new Vue({
　　　　el:"#demo",
　　　　data:{
　　　　　　classA:"class-a",
　　　　　　classB:"class-b"
　　　　}
})
```

3）、字符串绑定方式

```html
<div id="demo">
　　<span :class="classA"></span>
</div>

var vm = new Vue({
　　　　el:"#demo",
　　　　data:{
　　　　　　classA:"string"
　　　　}
})
```



> 响应式的--->简而言之，就是一个网站能够兼容多个终端

## 三、声明式渲染

Vue.js的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进DOM的系统：

```html
<div id="app">
    {{message}}
</div>
 
var app = new Vue({
	el:'#app',
	data:{
		message:'hello vue!'
	}
})
```

`v-bind` attribute 被称为**指令**。指令带有前缀 `v-`，以表示它们是 Vue 提供的特殊 attribute。可能你已经猜到了，它们会在渲染的 DOM 上应用特殊的响应式行为。在这里，该指令的意思是：“将这个元素节点的 `title` attribute 和 Vue 实例的 `message` 属性保持一致”。

## 四、条件和循环

### 1、v-if

```html
<div id="app-3">
  <p v-if="seen">现在你看到我了</p>
</div>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

### 2、v-for

```html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
  }
})
```

## 五、处理用户输入

为了让用户和你的应用进行交互， 我们可以用v-on指令添加一个事件监听器，通过它调用在Vue实例中定义的方法：

```html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">反转消息</button>
</div>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```

### 1、v-model

```html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
```

v-model 让指令，它能轻松实现表单输入和应用之间的双向绑定。

## 六、组件化应用构建

组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、独立和通常可复用的组件构建大型应用。仔细想想，几乎任意类型的应用界面都可以抽象为一个组件树：



除了数据属性，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 `$`，以便与用户定义的属性区分开来。



不要在选项属性或回调上使用[箭头函数](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)，比如 `created: () => console.log(this.a)` 或 `vm.$watch('a', newValue => this.myMethod())`。因为箭头函数并没有 `this`，`this` 会作为变量一直向上级词法作用域查找，直至找到为止，经常导致 `Uncaught TypeError: Cannot read property of undefined` 或 `Uncaught TypeError: this.myMethod is not a function` 之类的错误。