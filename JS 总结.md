# JS 总结

## JS判断数据类型

```javascript
1、typeof 最常见的判断方法
	其中typeof返回的类型都是字符串形式，需注意；
	另外typeof可以判断function的类型；在判断除Object类型的对象时比较方便。
2、instanceof	判断已知对象类型的方法
	instanceof后面一定要是对象类型，并且大小写不能错，该方法适合一些条件选择或分支。
	例如： c instanceof Array
3、根据对象的constructor判断：constructor
	注意：constructor 在类继承时会出错
4、通用但很繁琐的方法： prototype
	- 大小写不能写错，比较麻烦，但胜在通用。
	- 通常情况下用typeof判断就可以了，遇到预知Object类型的情况可以选用instanceof或constructor方法

```

## JS数据类型

```javascript
一、初始数据类型
	1.数值：number
	2.字符串：string
	3.布尔值: boolean ：true，false
	4.undefined: 未定义或不存在，即没有任何值
	5.null：表示空缺，即此处应该有一个值，暂时没有
二、引用数据类型
	1.object：对象
```

## 内存中一共分为几种对象

```
变量
DOM对象
常量
自定义对象
```

## 数据类型转换

```javascript
1、toString（）：转换为字符串，在JS中所有数据类型都可以转换为字符串；
	var a = [1, 2, 3]; 	a.toString(); //"1,2,3"
     var o = {};		o.toString(); //"[object Object]"
        
2、parseInt（）：解析出一个string或者number类型的整数部分，没有返回NaN；
	 var n2 = "23hello";  parseInt(n2); //23
3、parseFloat（）：解析出一个string的浮点数部分，没有返回NaN；
	  var n1 = "1.2.3"; 	parseFloat(n1); //1.2
       var n2 = "1.2hello" 	 parseFloat(n2); //1.2
       var n3 = "hello" 	 parseFloat(n3); //NaN 	 
```

## 强制类型转换

```javascript
1、Boolean(value) ：把指定的值转换成Boolean型；.
		Boolean({}); //true
      	 Boolean(null); //false
2、Number(value): 把指定的值转换成数字（可以是整数或浮点数）；
		Number("123"); //123
       	 Number("123h"); //NaN
      	 Number(true); //1
     	 Number(false); //0
       	 Number(undefined); //NaN
      	 Number(null); //0
      	 Number([]); //0
       	 Number({}); //NaN
3、String(value): 把给定的值转换成字符串
		String(123); //"123"
         String([1,2]); //"1,2"
      	 String(undefined) //"undefined"
       	 String(null) //"null"
      	 String({}) //"[object Object]"
```

## 隐式转换

```javascript
1、数字 + 字符串：数字转换成字符串； console.log(12+'12');//1212
2、数字 + 布尔值：true转换为1，false转换为0，							console.log(12+true);//13
3、字符串 + 布尔值：布尔值转换为true或false；
		console.log("hello" + true)//hellotrue
4、布尔值 + 布尔值; console.log(true + true);//2
```

## null和undefined

```javascript
1、undefined 
	表示一种未知状态，声明了但没有初始化的变量，变量的值时一个未知状态。访问不存在的属性或对象window.xxx）方法没有明确返回值时，返回值是一个undefined.当对未声明的变量应用typeof运算符时，显示为undefined。
2、null
	表示尚未存在的对象,null是一个有特殊意义的值。可以为变量赋值为null，此时变量的值为“已知状态”(不是undefined)，即null。（用来初始化变量，清除变量内容，释放内存）

    undefined==null   //结果为true,但含义不同。
 	undefined===null //false,两者类型不一致，前者为“undefined”，后者为“object”
```

## 运算符

```
- 1、运算符
- 算术运算符(+,-,*,/,%,++,--)
- 如果+号左边和右边有一边是字符串类型的数据的话，这个时候就变成字符串拼接
- var str = "你好"+123;//你好123
- var count = 2;
- var str1 = "你叫了我第"-count+"次";//你叫了我第2次
- 如果引用所指的地方是null的话，那么在运算中就会自动变成0
- 2、赋值运算符*(=,-=,+=,`=,/=,%=`)
- 3、 比较运算符(==,===,!=,>,<,>=,<=)
  - 先执行表达式计算再赋值
  - ==和!=在比较之前首先让双方的值做隐士类型转换，===不转换
- 4、逻辑运算符(||,&&,!)
- 5、条件运算符(1>2?3:4)

```

## 日期型函数

###  声明

```javascript
var myDate = new Date(); //系统当前时间

var myDate = new Date(yyyy, mm, dd, hh, mm, ss);

var myDate = new Date(yyyy, mm, dd);

var myDate = new Date(“monthName dd, yyyy hh:mm:ss”);

var myDate = new Date(“monthName dd, yyyy”);

var myDate = new Date(epochMilliseconds);
```

### 获取时间的某部分

```javascript
var myDate = new Date();

myDate.getYear(); //获取当前年份(2位)

myDate.getFullYear(); //获取完整的年份(4位,1970-????)

myDate.getMonth(); //获取当前月份(0-11,0代表1月)

myDate.getDate(); //获取当前日(1-31)

myDate.getDay(); //获取当前星期X(0-6,0代表星期天)

myDate.getTime(); //获取当前时间(从1970.1.1开始的毫秒数) 时间戳！！

myDate.getHours(); //获取当前小时数(0-23)

myDate.getMinutes(); //获取当前分钟数(0-59)

myDate.getSeconds(); //获取当前秒数(0-59)

myDate.getMilliseconds(); //获取当前毫秒数(0-999)

myDate.toLocaleDateString(); //获取当前日期

myDate.toLocaleTimeString(); //获取当前时间

myDate.toLocaleString( ); //获取日期与时间
```



