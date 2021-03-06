# 前端面试题JavaScript 一

# 相关知识点

`数据类型、运算、对象、function、继承、闭包、作用域、原型链、事件、RegExp、JSON、Ajax、DOM、BOM、内存泄漏、跨域、异步加载、模板引擎、前端MVC、前端MVVM、路由、模块化、Http、Canvas、jQuery、ECMAScript 2015（ES6）、Node.js、AngularJS、Vue、React......`

# 题目&答案

- 介绍一下 JS 的基本数据类型。

```
Undefined、Null、Boolean、Number、String

```

- 介绍一下 JS 有哪些内置对象。

```
Object 是 JavaScript 中所有对象的父对象
数据封装类对象：Object、Array、Boolean、Number、String
其他对象：Function、Argument、Math、Date、RegExp、Error

```

- 列举几条 JavaScript 的基本代码规范。

```
（1）不要在同一行声明多个变量
（2）如果你不知道数组的长度，使用 push
（3）请使用 ===/!== 来比较 true/false 或者数值
（4）对字符串使用单引号 ''(因为大多时候我们的字符串。特别html会出现")
（5）使用对象字面量替代 new Array 这种形式
（6）绝对不要在一个非函数块里声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但是它们解析不同
（7）不要使用全局函数
（8）总是使用 var 来声明变量，如果不这么做将导致产生全局变量，我们要避免污染全局命名空间
（9）Switch 语句必须带有 default 分支
（10）使用 /**...*/ 进行多行注释，包括描述，指定类型以及参数值和返回值
（11）函数不应该有时候有返回值，有时候没有返回值
（12）语句结束一定要加分号
（13）for 循环必须使用大括号
（14）if 语句必须使用大括号
（15）for-in 循环中的变量应该使用 var 关键字明确限定作用域，从而避免作用域污染
（16）避免单个字符名，让你的变量名有描述意义
（17）当命名对象、函数和实例时使用驼峰命名规则
（18）给对象原型分配方法，而不是用一个新的对象覆盖原型，覆盖原型会使继承出现问题
（19）当给事件附加数据时，传入一个哈希而不是原始值，这可以让后面的贡献者加入更多数据到事件数据里，而不用找出并更新那个事件的事件处理器

```

- call和apply的作用是什么？区别是什么？

```
call和apply的功能基本相同，都是实现继承或者转换对象指针的作用；
唯一不通的是前者参数是罗列出来的，后者是存到数组中的；
call或apply功能就是实现继承的；与面向对象的继承extends功能相似；但写法不同；
语法：
.call(对象[,参数1，参数2,....]);//此地参数是指的是对象的参数，非方法的参数；
.apply(对象,参数数组)//参数数组的形式:[参数1，参数2,......]

```

- push()-pop()-shift()-unshift()分别是什么功能？

```
push 方法
将新元素添加到一个数组中，并返回数组的新长度值。
var a=[1,2,3,4];
a.push(5);
pop 方法
移除数组中的最后一个元素并返回该元素。
var a=[1,2,3,4];
a.pop();
shift 方法
移除数组中的第一个元素并返回该元素。
var a=[1,2];
alert(a.shift());
unshift 方法
将指定的元素插入数组开始位置并返回该数组。

```

- 试写出大于1024并小于1360屏幕的媒体查询关键CSS代码

```
if ((screen.width == 1360) && (screen.height == 1024)){
    setActiveStyleSheet(CSS1);
}

```

- 表述您对javascript this工作原理的理解

```
在函数中：this 通常是一个隐含的参数。
在函数外（顶级作用域中）：在浏览器中this 指的是全局对象；在Node.js中指的是模块(module)的导出(exports)。
传递到eval()中的字符串：如果eval()是被直接调用的，this 指的是当前对象；如果eval()是被间接调用的，this 就是指全局对象。

```

- 介绍一下 JavaScript 原型，原型链，它们有何特点？

```
每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念。
关系：instance.constructor.prototype = instance.__proto__
特点：JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本，当我们修改原型时，与之相关的对象也会继承这一改变。
当我们需要一个属性时，JavaScript引擎会先看当前对象中是否有这个属性，如果没有的话，就会查找它的prototype对象是否有这个属性，如此递推下去，一致检索到Object内建对象。
function Func(){}
Func.prototype.name = "Xiaosong";
Func.prototype.getInfo = function() {
   return this.name;
}
var person = new Func();
console.log(person.getInfo());//"Xiaosong"
console.log(Func.prototype);//Func { name = "Xiaosong", getInfo = function() }

```

- JavaScript 有几种类型的值？能否画一下它们的内存图？

```
栈：原始数据类型（Undefined，Null，Boolean，Number，String）
堆：引用数据类型（对象、数组、函数）
两种类型的区别：
//存储位置不同
原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体。

```

JavaScript 如何实现继承？

```
(1)构造继承
(2)原型继承
(3)实例继承
(4)拷贝继承
//原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。
function Parent() { 
    this.name = 'song';
}
function Child() {
    this.age = 28;
}
Child.prototype = new Parent(); //通过原型,继承了Parent
var demo = new Child();
alert(demo.age);
alert(demo.name); //得到被继承的属性

```

- JavaScript 有哪几种创建对象的方式？

```
javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用。
//
(1)对象字面量的方式
person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};
(2)用function来模拟无参的构造函数
function Person(){}
var person = new Person(); //定义一个function，如果使用new"实例化",该function可以看作是一个Class
person.name = "Xiaosong";
person.age = "23";
person.work = function() {
     alert("Hello " + person.name);
}
person.work();
(3)用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）
function Person(name,age,hobby) { 
    this.name = name; //this作用域：当前对象
    this.age = age; 
    this.work = work; 
    this.info = function() { 
        alert("我叫" + this.name + "，今年" + this.age + "岁，是个" + this.work); 
    }
}
var Xiaosong = new Person("WooKong",23,"程序猿"); //实例化、创建对象
Xiaosong.info(); //调用info()方法
(4)用工厂方式来创建（内置对象）
var jsCreater = new Object();
jsCreater.name = "Brendan Eich"; //JavaScript的发明者
jsCreater.work = "JavaScript";
jsCreater.info = function() { 
    alert("我是"+this.work+"的发明者"+this.name);
}
jsCreater.info();
(5)用原型方式来创建
function Standard(){}
Standard.prototype.name = "ECMAScript";
Standard.prototype.event = function() { 
    alert(this.name+"是脚本语言标准规范");
}
var jiaoben = new Standard();
jiaoben.event();
(6)用混合方式来创建
function iPhone(name,event) {
     this.name = name;
     this.event = event;
}
iPhone.prototype.sell = function() { 
    alert("我是"+this.name+"，我是iPhone5s的"+this.event+"~ haha!");
}
var SE = new iPhone("iPhone SE","官方翻新机");
SE.sell();

```

- eval 是做什么的？

```
它的功能是把对应的字符串解析成JS代码并运行；
应该避免使用eval，因为不安全，非常耗性能（2次，一次解析成js语句，一次执行）。

```

- null 和 undefined 有何区别？

```
null 表示一个对象被定义了，值为“空值”；
undefined 表示不存在这个值。
typeof undefined //"undefined"
undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined； 
例如变量被声明了，但没有赋值时，就等于undefined。
typeof null //"object" 
null : 是一个对象(空对象, 没有任何属性和方法)； 
例如作为函数的参数，表示该函数的参数不是对象；
注意： 在验证null时，一定要使用　=== ，因为 == 无法分别 null 和　undefined

```

- 能否写一个通用的事件侦听器函数？

```
//Event工具集，from:github.com/markyunmarkyun.
Event = {
     //页面加载完成后
     readyEvent: function(fn) {
         if (fn == null) {
             fn = document;
         } 
      var oldonload = window.onload; 
      if (typeof window.onload != 'function') {
           window.onload = fn; 
      }else{
           window.onload = function() { 
              oldonload(); 
              fn();
           }; 
      }
    }, 
      //视能力分别使用 demo0 || demo1 || IE 方式来绑定事件 
      //参数：操作的元素，事件名称，事件处理程序 
      addEvent: function(element,type,handler) { 
          if (element.addEventListener) { //事件类型、需要执行的函数、是否捕捉   
               element.addEventListener(type,handler,false); 
          }else if (element.attachEvent) { 
              element.attachEvent('on' + type, function() {
                    handler.call(element);
               }); 
          }else { 
              element['on' + type] = handler; 
          }
       }, 
      //移除事件 
       removeEvent: function(element,type,handler) {
          if (element.removeEventListener) {
               element.removeEventListener(type,handler,false); 
          }else if (element.datachEvent) { 
               element.datachEvent('on' + type,handler); 
          }else{
               element['on' + type] = null;
          }
        },
     //阻止事件（主要是事件冒泡，因为IE不支持事件捕获） 
      stopPropagation: function(ev) { 
          if (ev.stopPropagation) { 
               ev.stopPropagation(); 
          }else { 
               ev.cancelBubble = true;
          }
       }, 
     //取消事件的默认行为
      preventDefault: function(event) {
         if (event.preventDefault) { 
              event.preventDefault(); 
         }else{
              event.returnValue = false; 
         }
      }, 
     //获取事件目标 
     getTarget: function(event) { 
        return event.target || event.srcElemnt; 
     },
     //获取event对象的引用，取到事件的所有信息，确保随时能使用event； 
     getEvent: function(e) { 
        var ev = e || window.event;
        if (!ev) { 
            var c = this.getEvent.caller; 
            while(c) { 
                ev = c.argument[0]; 
                if (ev && Event == ev.constructor) {
                     break; 
                } 
                c = c.caller; 
            } 
        } 
        retrun ev; 
      }
};

```

- ["1","2","3"].map(parseInt) 的答案是多少？

```
[1,NaN,NaN]
因为 parseInt 需要两个参数(val,radix)，其中 radix 表示解析时用的基数。
map 传了3个(element,index,array)，对应的 radix 不合法导致解析失败。

```

- 事件是什么？IE与火狐的事件机制有何区别？如何阻止冒泡？

```
(1)我们在网页中的某个操作（有的操作对应多个事件）。
    例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。
(2)事件处理机制：IE是事件冒泡、Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件；
(3)ev.stopPropagation();（旧ie的方法 ev.cancelBubble = true;）

```

- 什么是闭包(closure)，为什么要用它？

```
闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量，利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。
//闭包特性：
(1)函数内再嵌套函数
(2)内部函数可以引用外层的参数和变量
(3)参数和变量不会被垃圾回收机制回收
//li节点的onclick事件都能正确的弹出当前被点击的li索引
<ul> 
    <li> index = 0 </li> 
    <li> index = 1 </li> 
    <li> index = 2 </li> 
    <li> index = 3 </li>
</ul>
<script type="text/javascript"> 
    var nodes = document.getElementsByTagName('li'); 
    for(i = 0;i<nodes.length;i+=1) { 
        nodes[i].onclick = function() { 
            console.log(i+1); //不使用闭包的话，值每次都是4 
        }(4);
     }
</script>

```

- JavaScript 代码中的 "use strict"; 是什么意思？使用它的区别是什么？

```
use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行,使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为。
默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值;
全局变量的显示声明,函数必须声明在顶层，不允许在非函数代码块内声明函数,arguments.callee也不允许使用；
消除代码运行的一些不安全之处，保证代码运行的安全,限制函数中的arguments修改，严格模式下的eval函数的行为和非严格模式的也不相同;
提高编译器效率，增加运行速度；
为未来新版本的Javascript标准化做铺垫。

```

- new 操作符具体干了什么呢？

```
(1)创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
(2)属性和方法被加入到 this 引用的对象中。
(3)新创建的对象由 this 所引用，并且最后隐式的返回 this 。
//
var obj = {};
obj.__proto__ = Base.prototype;
Base.call(obj);

```

- JavaScript 中，有一个函数，执行对象查找时，永远不会去查找原型，这个函数是哪个？

```
hasOwnProperty
//
JavaScript 中 hasOwnProperty 函数方法是返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性；该属性必须是对象本身的一个成员。
//
使用方法：object.hasOwnProperty(proName)其中参数object是必选项，一个对象的实例。proName是必选项，一个属性名称的字符串值。
//
如果 object 具有指定名称的属性，那么JavaScript中hasOwnProperty函数方法返回 true，反之则返回 false。

```

- 你对 JSON 了解吗？

```
JSON(JavaScript Object Notation)是一种轻量级的数据交换格式。
它是基于JavaScript的一个子集。数据格式简单，易于读写，占用带宽小。
如：{"age":"12", "name":"back"}

```

- Ajax 是什么？如何创建一个 Ajax ？

```
ajax的全称：Asynchronous Javascript And XML，异步传输+js+xml。
所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。
//
(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象
(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息
(3)设置响应HTTP请求状态变化的函数
(4)发送HTTP请求
(5)获取异步调用返回的数据
(6)使用JavaScript和DOM实现局部刷新

```

- 同步和异步的区别？

```
同步的概念应该是来自于操作系统中关于同步的概念:不同进程为协同完成某项工作而在先后次序上调整(通过阻塞,唤醒等方式)。
同步强调的是顺序性，谁先谁后；异步则不存在这种顺序性。
//
同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,进行下一步操作。
//
异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容。

```

- 如何解决跨域问题？

```
jsonp、iframe、window.name、window.postMessage、服务器上设置代理页面

```

- 谈一谈你对 ECMAScript6 的了解？

```
ECMAScript 6 是JavaScript语言的下一代标准，已经在2015年6月正式发布了。
它的目标，是使得JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言。
标准的制定者有计划，以后每年发布一次标准，使用年份作为标准的版本。
因为当前版本的ES6是在2015年发布的，所以又称ECMAScript 2015。
也就是说，ES6就是ES2015

```

- ECMAScript 6 怎么写 class ，为何会出现 class？

```
ES6的class可以看作只是一个语法糖，它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。
//定义类
class Point { 
    constructor(x,y) { 
        //构造方法
         this.x = x; //this关键字代表实例对象
         this.y = y; 
    } toString() {
         return '(' + this.x + ',' + this.y + ')'; 
    }
}

```

- 异步加载 JS 的方式有哪些？

  ```

  ```

(1)defer，只支持 IE
(2)async:
(3)创建 script，插入到 DOM 中，加载完毕后 callBack

```
- document.write 和 innerHTML 有何区别？

```

document.write 只能重绘整个页面innerHTML 可以重绘页面的一部分

```
- DOM 操作——怎样添加、移除、移动、复制、创建和查找节点？

```

(1)创建新节点
createDocumentFragment() //创建一个DOM片段
createElement() //创建一个具体的元素
createTextNode() //创建一个文本节点
(2)添加、移除、替换、插入
appendChild()
removeChild()
replaceChild()
insertBefore() //在已有的子节点前插入一个新的子节点
(3)查找
getElementsByTagName() //通过标签名称
getElementsByName() //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
getElementById() //通过元素Id，唯一性

```
如何编写高性能 JavaScript ？详细文章：[浅谈编写高性能的Javascript代码](http://developer.51cto.com/art/200906/131335.htm)
- 哪些操作会造成内存泄漏？

```

内存泄漏是指任何对象在您不再拥有或需要它之后任然存在。
垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量，如果一个对象的引用数量为0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。
//
setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

```
jQuery 中如何将数组转化为 json 字符串，然后再转化回来？

```

jQuery 中没有提供这个功能，所以需要先编写两个 jQuery 的扩展：
$.fn.stringifyArray = function(array) {
return JSON.stringify(array)
}
$.fn.parseArray = function(array) {
return JSON.parse(array)
}
//然后调用:
$("").stringifyArray(array)

```
- jQuery.extend 与 jQuery.fn.extend 有何区别？

```

jQuery.extend(object);　//为jQuery类添加类方法，可以理解为添加静态方法
jQuery.extend({
min: function(a, b) { return a < b ? a : b; },
max: function(a, b) { return a > b ? a : b; }
});
jQuery.min(2,3); //  2
jQuery.max(4,5); //  5
jQuery.extend( target, object1, [objectN])用一个或多个其他对象来扩展一个对象，返回被扩展的对象
jQuery.fn.extend(object); //对jQuery.prototype进行的扩展，就是为jQuery类添加“成员函数”。jQuery类的实例可以使用这个“成员函数”。
比如我们要开发一个插件，做一个特殊的编辑框，当它被点击时，便alert 当前编辑框里的内容。可以这么做：
$.fn.extend({
alertWhileClick:function() {
$(this).click(function(){
alert($(this).val());
});
}
});
$("#input1").alertWhileClick(); // 页面上为$("#input1")为一个jQuery实例，当它调用成员方法 alertWhileClick后，便实现了扩展，每次被点击时它会先弹出目前编辑里的内容。

```
- 是否了解针对 jQuery 性能的优化方法？

```

基于Class的选择性的性能相对于Id选择器开销很大，因为需遍历所有DOM元素。
//
频繁操作的DOM，先缓存起来再操作。用Jquery的链式调用更好。
比如：var str=$("a").attr("href");
//
for (var i = size; i < arr.length; i++) {}
for 循环每一次循环都查找了数组 (arr) 的.length 属性，在开始循环的时候设置一个变量来存储这个数字，可以让循环跑得更快：
for (var i = size, length = arr.length; i < length; i++) {}

```
- jQuery 与 jQuery UI 有何区别？

```

jQuery是一个js库，主要提供的功能是选择器，属性修改和事件绑定等等。
jQuery UI则是在jQuery的基础上，利用jQuery的扩展性，设计的插件。提供了一些常用的界面元素，诸如对话框、拖动行为、改变大小行为等等

```
- 如何判断当前脚本运行在浏览器还是 node 环境中？（阿里）

```

通过判断 Global 对象是否为 window ，如果不为 window ，当前脚本没有运行在浏览器中

```
- 怎样用js实现千位分隔符？

```

正则 + replace
function commafy(num) {
num = num + '';
var reg = /(-?d+)(d{3})/;
if (reg.test(num)) {
num = num.replace(reg, '$1,$2');
}
return num;
}

```
- 检测浏览器版本有哪些方式？

```

功能检测、userAgent 特征检测
比如：navigator.userAgent
//"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"

```
- Canvas和SVG的比较；

```

| Canvas                                             | SVG                                  |
| -------------------------------------------------- | ------------------------------------ |
| 位图技术，可以保存为.png                           | 矢量图技术，不能保存为位图           |
| ---------------------------------                  | -----------------------------------  |
| 善于表现颜色和线条细节                             | 可以缩放，不善于表现细节             |
| ---------------------------------                  | -----------------------------------  |
| 网页游戏，统计图                                   | 图标，统计图，地图                   |
| ---------------------------------                  | -----------------------------------  |
| 一个标签(canvas)+一个对象(getcontext)，            |                                      |
| 所有图形图像都靠ctx绘制                            | 几十个标签---每个图形对应一个标签    |
| ---------------------------------                  | -----------------------------------  |
| 不能被搜索引擎爬虫所访问                      可以 |                                      |
| ---------------------------------                  | -----------------------------------  |
| 只能为整个 Canvas绑定监听函数                      | 每个图形（标签）可以绑定事件监听函数 |
| ---------------------------------                  | -----------------------------------  |

```
- 谈谈你对 JavaScript 中的模块规范 CommonJS、AMD、CMD 的了解？

```

| CommonJS | AMD       | CMD   |
| -------- | --------- | ----- |
| Node.js  | RequireJS | SeaJS |

//个人拙见

| CommonJS | AMD       | CMD   |
| -------- | --------- | ----- |
| Node.js  | RequireJS | SeaJS |

```
详细文章：[浅析JS中的模块规范（CommonJS，AMD，CMD）](http://www.2cto.com/kf/201411/348276.html)、[关于 CommonJS AMD CMD UMD](http://my.oschina.net/felumanman/blog/263330?p=1)

- 前端 MVC、MVVM
1、MVC
![](http://upload-images.jianshu.io/upload_images/4749582-b49cc8f09e938eaa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)MVC

```

模型（Model）：数据保存
视图（View）：用户界面
控制器（Controller）：业务逻辑
(1)View 传送指令到 Controller
(2)Controller 完成业务逻辑后，要求 Model 改变状态
(3)Model 将新的数据发送到 View ，用户得到反馈所有通信都是单向的。

```
2、MVVM
![](http://upload-images.jianshu.io/upload_images/4749582-5f80f772360f2ca8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)MVVM

```

模型（Model）
视图（View）
视图模型（ViewModel）
(1)各部分间都是双向通信
(2)View 与 Model 不发生联系，都通过 ViewModel 传递
(3)View 非常薄，不部署任何业务逻辑，称为“被动视图”（Passive View），即没有任何主动性；而 ViewModel 非常厚，所有逻辑都部署在那里。
采用双向绑定（data-binding）：View 的变动，自动反映在 ViewModel ，反之亦然。

```
- HTTP协议的状态消息都有哪些?(如200、302对应的描述)国内外的JS牛人都知道哪些?

```

协议是指计算机通信网络中两台计算机之间进行通信所必须共同遵守的规定或规则，超文本传输协议(HTTP)是一种通信协议，它允许将超文本标记语言(HTML)文档从Web服务器传送到客户端的浏览器，
• “100″ : Continue（继续） 初始的请求已经接受，客户应当继续发送请求的其余部分。（HTTP 1.1新）
•  “101″ : Switching Protocols（切换协议） 请求者已要求服务器切换协议，服务器已确认并准备进行切换。（HTTP 1.1新）
•  “200″ : OK（成功） 一切正常，对GET和POST请求的应答文档跟在后面。
•  “201″ : Created（已创建）服务器已经创建了文档，Location头给出了它的URL。
•  “202″ : Accepted（已接受）服务器已接受了请求，但尚未对其进行处理。
•  “203″ : Non-Authoritative Information（非授权信息） 文档已经正常地返回，但一些应答头可能不正确，可能来自另一来源 。（HTTP 1.1新）。
•  “204″ : No Content（无内容）未返回任何内容，浏览器应该继续显示原来的文档。
•  “205″ : Reset Content（重置内容）没有新的内容，但浏览器应该重置它所显示的内容。用来强制浏览器清除表单输入内容（HTTP 1.1新）。
•  “206″ : Partial Content（部分内容）服务器成功处理了部分 GET 请求。（HTTP 1.1新）
•  “300″ : Multiple Choices（多种选择）客户请求的文档可以在多个位置找到，这些位置已经在返回的文档内列出。如果服务器要提出优先选择，则应该在Location应答头指明。
•  “301″ : Moved Permanently（永久移动）请求的网页已被永久移动到新位置。服务器返回此响应（作为对 GET 或 HEAD 请求的响应）时，会自动将请求者转到新位置。
•  “302″ : Found（临时移动）类似于301，但新的URL应该被视为临时性的替代，而不是永久性的。注意，在HTTP1.0中对应的状态信息是“Moved Temporatily”，出现该状态代码时，浏览器能够自动访问新的URL，因此它是一个很有用的状态代码。注意这个状态代码有时候可以和301替换使用。例如，如果浏览器错误地请求[http://host/~user](https://link.jianshu.com?t=http://host/~user)（缺少了后面的斜杠），有的服务器返回301，有的则返回302。严格地说，我们只能假定只有当原来的请求是GET时浏览器才会自动重定向。请参见307。
•  “303″ : See Other（查看其他位置）类似于301/302，不同之处在于，如果原来的请求是POST，Location头指定的重定向目标文档应该通过GET提取（HTTP 1.1新）。
•  “304″ : Not Modified（未修改）自从上次请求后，请求的网页未被修改过。原来缓冲的文档还可以继续使用，不会返回网页内容。
•  “305″ : Use Proxy（使用代理）只能使用代理访问请求的网页。如果服务器返回此响应，那么，服务器还会指明请求者应当使用的代理。（HTTP 1.1新）
•  “307″ : Temporary Redirect（临时重定向）和 302（Found）相同。许多浏览器会错误地响应302应答进行重定向，即使原来的请求是POST，即使它实际上只能在POST请求的应答是303时才能重定向。由于这个原因，HTTP 1.1新增了307，以便更加清除地区分几个状态代码：当出现303应答时，浏览器可以跟随重定向的GET和POST请求；如果是307应答，则浏览器只能跟随对GET请求的重定向。（HTTP 1.1新）
•  “400″ : Bad Request（错误请求）请求出现语法错误。
•  “401″ : Unauthorized（未授权）客户试图未经授权访问受密码保护的页面。应答中会包含一个WWW-Authenticate头，浏览器据此显示用户名字/密码对话框，然后在填写合适的Authorization头后再次发出请求。
•  “403″ : Forbidden（已禁止） 资源不可用。服务器理解客户的请求，但拒绝处理它。通常由于服务器上文件或目录的权限设置导致。
•  “404″ : Not Found（未找到）无法找到指定位置的资源。
•  “405″ : Method Not Allowed（方法禁用）请求方法（GET、POST、HEAD、DELETE、PUT、TRACE等）禁用。（HTTP 1.1新）
•  “406″ : Not Acceptable（不接受）指定的资源已经找到，但它的MIME类型和客户在Accpet头中所指定的不兼容（HTTP 1.1新）。
•  “407″ : Proxy Authentication Required（需要代理授权）类似于401，表示客户必须先经过代理服务器的授权。（HTTP 1.1新）
•  “408″ : Request Time-out（请求超时）服务器等候请求时超时。（HTTP 1.1新）
•  “409″ : Conflict（冲突）通常和PUT请求有关。由于请求和资源的当前状态相冲突，因此请求不能成功。（HTTP 1.1新）
•  “410″ : Gone（已删除）如果请求的资源已被永久删除，那么，服务器会返回此响应。该代码与 404（未找到）代码类似，但在资源以前有但现在已经不复存在的情况下，有时会替代 404 代码出现。如果资源已被永久删除，那么，您应当使用 301 代码指定该资源的新位置。（HTTP 1.1新）
•  “411″ : Length Required（需要有效长度）不会接受包含无效内容长度标头字段的请求。（HTTP 1.1新）
•  “412″ : Precondition Failed（未满足前提条件）服务器未满足请求者在请求中设置的其中一个前提条件。（HTTP 1.1新）
•  “413″ : Request Entity Too Large（请求实体过大）请求实体过大，已超出服务器的处理能力。如果服务器认为自己能够稍后再处理该请求，则应该提供一个Retry-After头。（HTTP 1.1新）
•  “414″ : Request-URI Too Large（请求的 URI 过长）请求的 URI（通常为网址）过长，服务器无法进行处理。
•  “415″ : Unsupported Media Type（不支持的媒体类型）请求的格式不受请求页面的支持。
•  “416″ : Requested range not satisfiable（请求范围不符合要求）服务器不能满足客户在请求中指定的Range头。（HTTP 1.1新）
•  “417″ : Expectation Failed（未满足期望值）服务器未满足”期望”请求标头字段的要求。
•  “500″ : Internal Server Error（服务器内部错误）服务器遇到错误，无法完成请求。
•  “501″ : Not Implemented（尚未实施） 服务器不具备完成请求的功能。例如，当服务器无法识别请求方法时，服务器可能会返回此代码。
•  “502″ : Bad Gateway（错误网关）服务器作为网关或者代理时，为了完成请求访问下一个服务器，但该服务器返回了非法的应答。
•  “503″ : Service Unavailable（服务不可用）服务器由于维护或者负载过重未能应答。通常，这只是一种暂时的状态。
•  “504″ : Gateway Time-out（网关超时） 由作为代理或网关的服务器使用，表示不能及时地从远程服务器获得应答。（HTTP 1.1新）
•  “505″ : HTTP Version not supported（HTTP 版本不受支持）不支持请求中所使用的 HTTP 协议版本。
国内的比较牛的人：淘宝网UED官方博客。灵玉，大成小胖，承玉，拔赤