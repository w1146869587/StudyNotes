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

### 1、插值

