# JS 复习

## 异常捕获

```javascript
try{
    发生异常的代码块
}catch(err){
    console.log(err)
	错误信息处理
}
Throw语句：
if(err) throw err;
```

## 事件

onClick				点击事件

onMouseOver			鼠标经过事件

onMouseOut			鼠标移出事件

onChange			文本内容改变事件

onSelect				文本框选中事件

onFocus				光标聚焦事件

onBlur				失去光标事件

onLoad				网页加载事件

onUnload			关闭网页事件

## DOM

### DOM操作HTML

改变HTML输出流：注意：： 绝对不要在文档加载完成后使用document.write(),会覆盖原文档

操作属性 ： attribute



### DOM Eventlistener

addEventlistener("事件名","事件处理函数","布尔值")

true:事件捕获    	false:事件冒泡

removeEventlistener

## 事件对象

事件对象：

1）type：获取事件类型

2）target：获取事件目标

3）stopPropagation（）：阻止事件冒泡

4）preventDefault（）：阻止事件默认行为

## window

window.open("打开的页面","名称","样式") 打开页面

window.close(); 关闭页面

window.history 对象

history.back()回退

history.forward() 跳转下一个页面

history.go()

window.location对象 用于获取当前页面地址，并重定向到新的页面

location.hostname 返回主机的域名

location.pathname 返回当前页面的路径和文件名

location.port 返回web主机的端口号

location.protocol 返回使用的web协议

location.href返回当前页的URL

location.assign() 方法加载新的文档

window.screen 对象包含有关屏幕的信息

screen.availWidth 可用的屏幕宽度

screen.availHeight 可用的屏幕高度

screen.Height 屏幕高度

screen.Width 屏幕宽度