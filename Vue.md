# Vue

## 安装命令

```
$ npm install -g vue-cli
$ vue init webpack my-project
$ cd my-project
$ npm install
$ npm run dev
```



```
javascript 框架
组件 mvvm双向数据绑定 
CDN：内容分发系统
指令：v-

生命周期钩子函数:钩子函数->回调函数
beforeCreate:创建之前   created:创建    beforeMount:挂载之前   mounted:挂载时

{{}}表达式:有值，有结果 

: -> v-bind  缩写
@ -> v-on  缩写

```

```javascript
new Vue({
    el:'#',//作用的一个范围
    data：{  // 对象 数据
		message:'',
	}，
    methods:{ // 方法 
   
    },
    computed:{// 计算属性  有缓存
        
    }    
})
```

## 数据

```
data:{
    
}
```



## 方法 mothods

```
methords:{
    
}
```



## 计算属性 computed

```javascript
计算属性 computed
	会有缓存，有依赖性

<div id="example">
  {{ message.split('').reverse().join('') }}
</div>
split 拆分； reverse：反转 ；  join：拼接

<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
        
    }
      
  }
})
```

## 侦听属性

```javascript


watch:{
    firstname:function(newv,oldv){
        //newv 改变的值    oldv 以前的值
    }，
    // 深度侦听
    handler: function (val, oldVal) { /* ... */ },
      deep: true
}
```

## 类与style的绑定

```javascript
v-bind  v-on
""内的都会解析成变量，"''" 加上''会解析成字符串;

v-bind:class="";   //动态的改变
对象:


```

## 条件渲染

```javascript
v-if v-else //连在一块用
key: 管理可重复的元素；

v-show  v-if

v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。
```

## 列表渲染

```javascript
v-for = "(item,index) in items"
 v-for 指令根据一组数组的选项列表进行渲染。v-for 指令需要使用 item in items 形式的特殊语法，items 是源数据数组并且 item 是数组元素迭代的别名。
 
 数组
   v-for = "(item,key,index) in items"
```

## 数组更新检测

```javascript
变异方法
Vue 包含一组观察数组的变异方法，所以它们也将会触发视图更新。这些方法如下：
push()
pop()
shift()
unshift()
splice()
sort()
reverse()

替换数组
filter()
concat() 
slice() 

```

## 事件处理

```javascript

事件修饰符
.stop
.prevent
.capture
.self
.once
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>

使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 v-on:click.prevent.self 会阻止所有的点击，而 v-on:click.self.prevent 只会阻止对元素自身的点击。

```

## 表单输入绑定

```
单个复选框，绑定到布尔值：
多个复选框，绑定到同一个数组：


值绑定：

修饰符：
.lazy
在默认情况下，v-model 在每次 input 事件触发后将输入框的值与数据进行同步 (除了上述输入法组合文字时)。你可以添加 lazy 修饰符，从而转变为使用 change 事件进行同步：
.number
如果想自动将用户的输入值转为数值类型，可以给 v-model 添加 number 修饰符：
.trim
如果要自动过滤用户输入的首尾空白字符，可以给 v-model 添加 trim 修饰符：

```

## 组件

```javascript
组件：
全局注册:
new Vue({
    Vue.component('name',{
    	template:'<div> {{number}} </div>',
    	// 模板 只能用一个根源素
    	data:function(){ // data 必须是一个函数
    		number:10,
		}
	})
})

局部注册：
new Vue({
    el:'#',
    components:{
        'name':{
            template:'<div> value </div>',
        }
    }
})
```

组件组合

父子组件的关系可以总结为 **prop 向下传递，事件向上传递**。父组件通过 **prop**给子组件下发数据，子组件通过**事件**给父组件发送消息

从上往下prop传递，从下往上通过事件

```javascript
props:['msg']  // 获取值

1、定义一个局部变量，并用 prop 的值初始化它：
props: ['msg'],
data: function () {
  return { 
      counter: object.assign({},this.msg);
      // object.assign 存对象 子元素改父元素不变
  	}
}

```

## 使用v-on绑定自定义事件

```javascript
子组件通过事件传到父组件
通过v-on绑定一个事件 自定义事件名 父组件
$emit('',''), 第一个是事件对象，第二个是参数
```

## 插槽

```jvascript
单个插槽

具名插槽
	<slot> 元素可以用一个特殊的特性 name 来进一步配置如何分发内	容。多个插槽可以有不同的名字。具名插槽将匹配内容片段中有对应 		slot 特性的元素。
    仍然可以有一个匿名插槽，它是默认插槽，作为找不到匹配的内容片段的	备用插槽。如果没有默认插槽，这些找不到匹配的内容片段将被抛弃。
    
    
作用域组件
	在父级中，具有特殊特性 slot-scope 的 <template> 元素必须存	在，表示它是作用域插槽的模板。slot-scope 的值将被用作一个临时变	量名，此变量接收从子组件传递过来的 
    
    
```

## 路由 router

```html
单页面应用 spa
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>

<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- 使用 router-link 组件来导航. -->
    <!-- 通过传入 `to` 属性指定链接. -->
    <!-- <router-link> 默认会被渲染成一个 `<a>` 标签 -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- 路由出口 -->
  <!-- 路由匹配到的组件将渲染在这里 -->
  <router-view></router-view>
</div>

```



```javascript
// 0. 如果使用模块化机制编程，导入Vue和VueRouter，要调用 Vue.use(VueRouter)

// 1. 定义（路由）组件。
// 可以从其他文件 import 进来
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. 定义路由
// 每个路由应该映射一个组件。 其中"component" 可以是
// 通过 Vue.extend() 创建的组件构造器，
// 或者，只是一个组件配置对象。
// 我们晚点再讨论嵌套路由。
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. 创建 router 实例，然后传 `routes` 配置
// 你还可以传别的配置参数, 不过先这么简单着吧。
const router = new VueRouter({
  routes // （缩写）相当于 routes: routes
})

// 4. 创建和挂载根实例。
// 记得要通过 router 配置参数注入路由，
// 从而让整个应用都有路由功能
const app = new Vue({
  router
}).$mount('#app')

// 现在，应用已经启动了！
```

```
数组删除
splice 下标位置 
filter 条件
```

