#### 1-1工具安装
工欲善其事，必先利其器，在使用 Vue 时，推荐在浏览器上安装 [Vue Devtools](https://github.com/vuejs/vue-devtools#vue-devtools)。你可以更好调试 Vue 应用。
vue可以直接引用最新版本```<script src="https://cdn.jsdelivr.net/npm/vue"></script>```
也可以下载到本地 [vue.js](https://vuejs.org/js/vue.js)
#### 1-2hello world
国际惯例先来个hello world [源码](https://github.com/CleanWaterjx/HelloVue/blob/master/VueLearn1/HelloVue.html)

```
<div id="app">{{message}}</div>	
```
```
  var app = new Vue({
		el:	'#app',
		data:{
			message:'hello Vue!'
    }
	})		

```

***对象的实例化包括以下三个部分***
- 实例化vue对象：new Vue
- el：element需要获取的元素，一定是html中的根容器元素
- data：用于数据的存储，是个对象，内部可以存各种数据

#### 1-3绑定(v-bind)
除了hello world中那样文本插值，我们还可以这样来绑定元素特性[源码](https://github.com/CleanWaterjx/HelloVue/blob/master/VueLearn1/Bind.html)

```	
 <div id="app-2">
	 <span v-bind:title="message">
	   鼠标悬停几秒钟查看此处动态绑定的提示信息！	
	 </span>
 </div>		
```
```
 var app2 = new Vue({
		el:'#app-2',
		data:{
			message: '页面加载于' + new Date().toLocaleString()			
    }
 })
```
#### 1-4条件和循环(v-if v-for)
[源码](https://github.com/CleanWaterjx/HelloVue/blob/master/VueLearn1/Conditional.html)

```
<div id="app-3">
  <p v-if="seen">现在你看到我了</p>
</div>
```
```
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```
在控制台输入 ```app3.seen = false``` 之前显示的消息会消失了，这说明了我们不仅可以把数据绑定到 DOM 文本或特性，还可以绑定到 DOM 结构
[源码](https://github.com/CleanWaterjx/HelloVue/blob/master/VueLearn1/loop.html)

```
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
```
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Learn JavaScript' },
      { text: 'Learn Vue' },
      { text: 'Build something awesome' }
    ]
  }
})
```
在控制台里，输入 ```app4.todos.push({ text: 'new item' })```表最后添加了一项。
#### 1-5事件绑定(v-on)与数据双向绑定(v-model)
[源码](https://github.com/CleanWaterjx/HelloVue/blob/master/VueLearn1/listener.html)

```
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```
```
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
在 reverseMessage 方法中，我们更新了应用的状态，但没有触碰 DOM——所有的 DOM 操作都由 Vue 来处理，我们编写的代码只需要关注逻辑层面即可

Vue 还提供了 v-model 指令，它能轻松实现表单输入和应用状态之间的双向绑定.[源码](https://github.com/CleanWaterjx/HelloVue/blob/master/VueLearn1/model.html)

```
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
```
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
```
#### 1-6组件
vue允许我们使用小型、独立和通常可复用的组件构建大型应用,也就是页面可以由好多部分组成，把页面切成一部分一部分，而拆分出来的部分，就是一个组件，就像搭积木一样。也可以理解为可以重复利用的结构层代码片段。[源码](https://github.com/CleanWaterjx/HelloVue/blob/master/VueLearn1/Composing.html)

```
数据的传递通过v-bind: 来定义传递的属性，后面跟上要传递的值
通过“props”来接受属性，再通过插值表达式来展示{{ todo.text}}
<div id = "app-7">
  <ol>
    <todo-item
      v-for = "item in groceryList"
      v-bind:todo = "item"
      v-bind:key = "item.id"
      ></todo-item>
  </ol>
</div>	
```
```
  //组键的定义
Vue.component('todo-item', {
  props: ['todo'],
  	template: '<li>{{ todo.text }}</li>'
})

```
```
var app7 = new Vue({
	el:'#app-7',
		data:{
			groceryList:[
				{id : 0,text : '蔬菜'},
				{id : 1,text : '奶酪'},
				{id : 2,text : '随便其他什么人吃的东西'}
			]
		}
})
```