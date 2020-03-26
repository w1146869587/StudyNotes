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

