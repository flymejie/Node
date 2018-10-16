# react

是一个视图 view

是一个库，虚拟的DOM

## react 环境搭建

```html
先引进react JS文件 循序不能反
react.development.js  react-dom.development.js  babel.min.js


<div id="app"></div>
// script type 要设置为 text/babel 、script内要用babel解析jsx类型
<script type="text/babel">
    ReactDOM.render(
    // 创建DOM
            <h1>hello word</h1>,
    document.querySelector('#app')
    // 创建到#app 中
    )

</script>

```

## 优势

构建用户界面的一个库

## 虚拟DOM

```
是一个对象，描述以什么样的方式显示
存在一种算法，先比较相同，不同点，渲染不同点，改变的
diff算法对比更新部分
组件 状态 渲染 render


```

## JSX

```
JSX : js扩展的语言
```

## 创建一个组件

```
最简单的定义组件的方法是写一个 JavaScript 函数:

function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
这个函数是一个有效的 React 组件，因为它接收一个 props 参数, 并返回一个 React 元素。 我们把此类组件称为”函数式(Functional)“组件， 因为从字面上看来它就是一个 JavaScript 函数。

你也可以用一个 ES6 的 class 来定义一个组件:

class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}


props 接收传递过来的对象 函数 props.name  类方法 this.props.name
注意：定义组件首字母要大写；
```

## 状态和生命周期函数

```
componentWillMount() 组件开始前执行
render() 开始渲染
componentDidMount() 钩子在组件输出被渲染到 DOM 之后运行

shouldComponentUpdate(nextProps,nextState) 运行中执行，返回布尔值  true 从新加载；false不加载   控制页面是否渲染 
	nextProps 下一对应的属性
	nextState 下一对应的状态
	
ReactDOM.unmountComponentAtNode(document.querySelector('#app'))	 卸载某元素
handleDelete(){         ReactDOM.unmountComponentAtNode(document.querySelector('#app'))
        }
```

## 事件

```
在 React 中你不能通过返回 false（愚人码头注：即 return false; 语句） 来阻止默认行为。必须明确调用 preventDefault 
```

## 绑定样式

```
双大括号
```

## 类

```
类里面必须有 constructor(){super()

}
```

# this指向

```
.bind(this)
let that = this
箭头函数:()=>{} this指向声明时

```

# 受控组件

```
要有默认值是必须要用受控组件
```

# 非受控组件

```
...在函数中是接收剩余参数
function（...rest）{
    ...rest 逆运算和剩余参数相反 拆成数组元素
}


```



