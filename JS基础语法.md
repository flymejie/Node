# 网页的组成（3部分）
* 结构层（html）
* 表现层（css）
* 行为层（javascript）

# 什么是编程？
	记录整个程序的过程就是编程。
## 什么是流程？
	做某个事情的过程就是流程
## 需求
	分析我们需要实现的功能
## 什么是程序？
	把做事情的过程写成一份文档就是程序，为了实现某个功能和目的，通过计算机语言编写的指令序列的集合。




# JavaScript/Java
* 公司：java-sun     JS-网景公司
* 语言执行：Java（强类型语言）强制性变量声明方式      JavaScript（弱类型语言）
* java是纯面向对象的（封装、继承、多态）；JavaScript是基于对象（一切皆对象），【内置对象：日期，数组。。。】
* 执行方式：java需要在虚拟机上去运行，是编译类型的；JavaScript是解释型的

# JS作用
##1. 实现动效
##2. 操作html、css
##3. 数据验证
##4. 制作游戏（）
##5. 单页面的应用
     （Google在线的word、excel等编辑器；各大平台的云）
##6. 服务器端的应用（node.js）
##7. cookie

# JavaScript是什么？
js是一个脚本语言（脚本语言可以在浏览器中执行，无需编译，执行顺序是从上到下解析，没用生命周期）
js是基于对象和事件驱动的、解释型的松散型语言。
## 基于对象（一切皆对象）
## 事件驱动：对浏览器和用户的行为进行响应
## 解释型：浏览器自身可以解析执行无需编译解析
## 松散型（弱类型）

# JS语言
 ## 如何执行

 ## html中引入JS的方式

    1.引入外部文件<script src=""></script>
      注意：标签内不能写入内容
    
    2.嵌入式
    3.在超链接以及重定向里面写入
    
      * 超链接的表现形式
        <!-- 普通链接 -->
          	<a href="http://"></a>
          	<!-- 在js里写入代码 -->
          	<a href="javascript:alert('1')"></a>
          	<a href="javascript:void(0)"></a>
          	<!-- 资源下载，默认只能是压缩过的文件 -->
          	<a href="1.zip"></a>
          	<!-- 空链接   点击后会跳转到页面顶部-->
          	<a href=""></a>
      * 重定向
        <form action="javascript:alert(1)" method="get">
          		<input type="submit">
          	</form>
    
    4.在事件之后调用
    
          <div onclick="alert(2)"></div>
    
          注意：多个script块之间会相互影响

##如何输出
###1.js输出工具
    a 把想要展示的数据输出至页面
    b 调试
    1. alert();在页面中弹出一个对话框。注意：alert()会阻止后面代码的执行
    2. console.log();将数据内容输出到控制台
    3. document.write();将数据内容输出到页面中
    注意：识别标签和行内样式
    4. confirm();在页面中弹出一个带确定和取消按钮的弹出框
    5. prompt('请输入你的姓名');页面中弹出一个带提示信息和输入框的弹出框


     * 注释标签

##变量
###命名规范：
      1. 变量必须以字母，下划线_或者$开头，后面部分可以跟任意的字母、数字、下划线_、或$;
      2. 不能使用关键字(JS自定义的var)或者是保留字(为以后扩展)命名；
      3. JavaScript有自己的命名习惯
          * * 驼峰命名法:getElementById
          * * 首字母大写法:object
      4. 变量名区分大小写
      5. 命名一定要有意义，提高代码的可读性
###什么是变量：
    变量是保存数据的一个容器。
    内存就是一个盒子，每次声明一个变量，它都会在内存中开辟一段空间进行保存。保存起来后
    当我们需要用的时候会从内存中获取相应的数据。如果浏览器关闭，内存会释放空间，方便下次使用。
###变量声明（通过关键字）:
    1. var
    2. let(ES6)
    	* let的用法类似于var
    	* let不存在变量提升现象
    	* let不能重新声明，报错该变量已经存在
    3. const(ES6)
    	* const声明的是一个常量
    	* const只能声明的同时进行赋值
    	* const也不存在变量提升现象
    	* const不能重新声明，报错该变量已经存在
###变量的赋值情况
    1. 声明变量的同时进行赋值
    2. 声明之后赋值
    3. 声明多个变量并同时进行赋值时使用逗号”,“隔开
    4. 声明多个变量之后赋值
    * 注意：
    1. 变量声明之前进行调用，会返回undefined。【变量提升现象】
    2. 不通过关键字声明的变量，但是赋值之后，它会返回对应的值。(全局变量)
    3. 不通过关键字声明的变量，没有赋值，会报错。
    4. 对变量重新赋值会覆盖之前的值。
    5. 重新声明相同的变量并进行赋值，会发生覆盖。

## 数据类型
    能够表达或者操作值的类型成为数据类型
###为何要划分数据类型？
	1. 需求
	2. 在内存中存储的位置不一样
###分类：
    一. 初始类型（存放于栈区，内存比较小，访问速度快）
        1. undefined
            可能的情况：声明变量并未赋值，返回undefined
    	    声明变量之前访问，返回undefined
        2. null（空，占位符）
            可能的值：null
            返回的值：null
            返回值的类型：object
        3. number（数值类型）
            整型、浮点型、二进制、八进制、十进制、十六进制、科学计数法
            返回的值：对应的数值
            返回值的类型number
        4. string（字符串类型）通过反引号引起来的
            返回的值：对应的字符串
            返回值的类型：string
        5. 布尔类型（boolean）  true、false
        6. symbol（es6）
    二. 引用类型（存放于堆区，内存大，访问速度慢）
        object（数组、函数）

 ## 运算符
 ###算术运算符（+ - * / % ++ -- ）
 #### + ：*  进行加法运算
        * 如果两个操作数都是number.最终得到number.
        * 如果其中一个操作数是underfined，最终得到NaN（not a number.是number的一个状态）
        * 如果其中一个操作数是null，最终得到number的值
        * 如果其中一个操作数是boolean，会转换成对应的值进行计算
        * 字符串连接
        * 如果操作数有一个是string（字符串）
  #### - ：* 进行减法运算
		* 如果两个操作数都是number.最终得到number.
		* 如果其中一个操作数是underfined，最终得到NaN（not a number是number的一个状态） 
		* 如果其中一个操作数是null，最终得到number的值 
		* 如果其中一个操作数是boolean，会转换成对应的值进行计算
		* 字符串连接
			* 如果操作数有一个是string（字符串）： 
		   		* 数值：隐式转换
		   		* 字母：会得到NaN
		   	* 如果两个操作数都是string（字符串），得到NaN

 ####  乘法： 
 			特殊用法： **进行幂运算

 #### ++ ：自增 num++ 先运行在自增1

 #### -- ：自减 num-- 先运行在自减1

 ### 比较运算符（关系运算符）（> < ==(等于) ===(全等于) >= <= !=（不等于））
		* 如果操作数是字符串类型，会先进行隐式转换，转换成功进行正常运算，转换不成功永远返回false
		* null == 0   false
	
		* undefined == null  true
		  undefined === null  false

### 赋值运算符(= += -= *= /= %=)
	var num1 = 20;
	num1 += 2;(num1 = num1 + 2)
### 逻辑运算符（&& 与      ||或     ！非）
		可以操作任何类型的数据
		数字0，false，undefined，null，NaN，空字符串会转换为false
	
		&&与 同真为真，其余全为假
		num1     num2       result      结果
		true     true       true        num2
		true     false      false	    num2
		false	 true	   false	    num1
		如果第一个操作数为假，发生短路原则，对第二个数不会进行操作，并返回假值。
		||或  同假为假 ，其余全为真
		num1     num2      result       结果
		false	false		false		num2
		true     true       true        num2
		true     false      true		num1
		false	 true		true		num1
		如果第一个数为真，发生短路原则，对第二个数不会进行操作并返回真数
 ### 其它运算符
        * 一元运算符
              (typeof ) 
        * 三元运算符
           条件表达式为真是的：为假的值
        * 特殊运算符（）
           作用 提高优先级
 ### 模板字符串
 		作用：方便引入变量
 		模板字符串要用反引号导起来，如果需要引入变量通过${（变量名）}
 		var num1 = 20;
 		var num2 = 30; 
 		console.log("这是num1--" num)                     
		console.log（ "这是num1..."$num ）

 ## 流程控制
 	### 流程
 		程序代码的执行顺序。
 		注意：JS的执行是根据浏览器的解析从上到下，一条语句一条语句的执行，有且只有一种方式。
 	### 流程控制
 		通过规定的语句让程序代码有条件的按照一定的方式执行
 	### 表达式
 		表达式一般由运算符和操作数构成，且有一定的值。（已经有值或即将赋值）
 	### 语句
 		以；为标识的一条语句
       * 声明语句（声明一个变量，数组...）
       * 赋值语句（对变量进行赋值）
             * if语句， switch语句，for语句等等
                  * 函数
        ### 三大流程控制
       1. 顺序结构
              	是程序中最基本的流程控制，默认从上到下，一条语句一条语句执行
       2. 选择结构
    
       *  分支结构
            if(条件){执行的语句 alert}
            if(){} else{}
            if(){} else if(){}else{}
            注意：条件可以是表达式也可以是任何数据类型
    
       * 条件结构
            switch(表达式){ case 条件1：条件1成立执行的语句；			break；
            case 条件2：条件2成立执行的语句；break；
              ...
            default：条件都不满足执行的语句				
              }
    
       3.循环结构
    
              当在条件满足的时候，需要重复的执行一段代码
            	 for(初始化变量；条件表达式；步操作){
             			执行的语句
             	}
    
            ```html
             for(var i = 0;i < 6; i++){
               for(var j = 0;j < 5-i; j++){
                 document.write(`&nbsp;`);
               }
               for(var k = 0;k < i+1; k++){
                 document.write(`*&nbsp; `);
               }
               document.write(`<br>`)
             }
            ```


​    
       *  while语句

           while（条件表达式）{要执行的语句}

          ```html
             var a = 1;
             while(a < 10){
               var b = 1;
               while(b <= a){
                 document.write(`${a}*${b}=${a*b}`);
                 document.write("&nbsp; ");
                 b++;
               }
               document.write(`<br>`);
               a++;
             }
          ```
    
       *  do while 语句
    
           总结：while和do while的区别
    
           while：满足条件才执行循环体；
    
           do while：先执行一次循环体，在进行判断


​    
           for和while

           *循环次数确定时用for

           *循环次数不确定时用while

           终止语句：

          * break：跳出整个循环（每次只能跳一层）

          * continue：跳出本层循环

              注意：最好用适当的语句替代continue语句

          * 一次跳出多次循环，在要跳出的那层循环前面加一个标记.

          比如：“out：” . 那么终止语句就是“break out；”

​          
 ## 数组
    一、数组
        变量：存储数据的容器
        数组：存储一组或者一系列相关数据的集合
    二、优势
        * 方便对数据进行管理
        * 可以保存大批量的数据
    
    三、创建方式
        1、json格式
           
        2、通过实例化对象的方式
            var arr = new Array（）;
        3、字面量
    	 var arr = [];
    四、赋值情况
        1、声明的同时进行赋值
            var arr = [34,65,];
        2、声明之后进行赋值 （通过下标赋值）
            var arr1 =[];
            arr1[0] = 34;
            arr1[1] = 65;
    
    五、对数组的访问
        以下标的形式进行访问
        * length属性：统计数组的长度
        * 访问数组的第一个元素：arr[0]
        * 访问数组最后一个元素：arr[arr.length-1]
    
    六、对数组的遍历
        * for
              for（初始化值；条件表达式；步操作）{
                   执行的语句
              }
        * for in
              一般用于数组和对象的遍历
              for（变量 in 对象）{
                
              }
           for(var i in arr.length)
              for in 最终遍历出来的是对象的属性
    
        注意：
        * 数组默认的值为空【变量默认值是undefined】
        * 数组的长度是可变的
        * 数组可以保存任何类型的数据
        * 数组下标是从0开始
    七、每个数组元素的值对应的也是元素的值
        1、二维数组的访问方式
            通过双下标
            
        2、二维数组的遍历，双层for循环
            var arr = [ [12,25,29],[31,38,39],[41,45,49]];
            for (var i = 0; i < arr.length; i++) {
                arr[i];
            }
            console.log(arr);
    
            var arr = [ [12,25,29],[31,38,39],[41,45,49]];
            for (var i = 0; i < arr.length; i++) {
                for (var a = 0; a < arr[i].length; a++) {
                    
                }
                console.log(arr[i]);
            }
    
        3、 浅拷贝和深拷贝
            浅拷贝：传的是地址，会改变。指向的是赋值对象的引用
    
            深拷贝：传的值,不会改变。指向的是赋值对象所有引用对象的引用。
    
            浅拷贝
            var arr = [1,2,3];
            var newarr = arr;
            console.log(newarr);
            newarr[1] = 30;
            console.log(arr);
            console.log(newarr);
    
            深拷贝
    
            var arr = [4,2,6];
            var newarr = [];
            for (var i = 0; i < arr.length; i++) {  
                newarr[newarr.length] = arr[i];
            }
            newarr[1] = 50;
            console.log(newarr);
            console.log(arr);
 ## 函数
 ###   一、函数
        函数就是将能够实现某一特定功能的代码块封装起来，方便重复调用。

 ###   二、特点
        程序会更加简洁，维护起来会更容易。

 ###   三、函数声明（3种方式）
        1、通过关键字
            function 函数名（【参数1】，【参数2】，【参数3】...）{
                函数体
            }
            【】代表可有可无
        2、通过字面量的方式
            var 变量名 = function（）{
                函数体
            }
        3、通过实例化对象的方式
            var 变量名 = new function（）；

 ###   四、函数的调用
        1、函数名/变量名 + （）
        2、函数自调用        
            （function 函数名（）{
                 函数体
            }  ）
            注意：函数自调用的时候，无论之前写的什么，必须加分号
        3、在事件之后调用
            只需要写函数名    

 ###   五、注意
        * 函数名重复会发生覆盖
        * 通过关键字声明的函数，可以在声明之前进行访问；通过自面量声明的函数只有在解析到它的时候，
            才会进行赋值。
        * 代码是从上到下一条语句一条语句解析执行。多个script块之间由于解析环境一样，它们之间是相互影响，
        * 调用不同块之间函数需要注意一定要先声明再调用。 

 ###   六、参数

         动态改变函数体内相对应的值和类型，实现不同效果
         形参：声明函数时（）里传的是形参
         实参：调用函数时（）里传的是实参 

 ###   七、有关参数的个数
        * 实参和形参一一对应
        * 实参个数< 形参：多余的形参返回undefined
        * 实参个数大于形参：只返回形参相对应的值

 ###   八、多余实参的接收
        1、reset参数    
            reset接收剩余参数的时候，作为一个数组进行处理
            
        2、arguments 对象
            当我们创建一个函数时，默认会创建一个 arguments 对象
            在arguments对象身上，保留了所有参数的信息
    		arguments.callee 指向函数自身 


            注意：...reset是运算符
            eg:function al(num, num1,...reset){
                    console.log(num,num1,reset);
            } 
 ###   九、默认参数设置
        1、直接在形参后面进行设置
       	 注意：默认参数位置一定放在最后
        2、通过三元运算符
            条件表达式？为真的值：为假的值
        3、逻辑或||

 ###   十、函数返回值
        return
        * 在函数调用的地方，返回一个值
            注意：如果return后没有值，返回undefined
                  return只能返回一个值，如果在return后跟多个值，
                  会发生覆盖，最终返回最后一个值
                  在函数里有多条return语句但只执行一条
        * 终止函数执行，return之后的语句都将不在执行

 ###   十一、作用域
        环境：
            宿主环境：浏览器
            执行环境：决定了变量和函数的访问权限
                全局环境
                函数环境
        作用域：有关变量和函数的访问范围
        作用域中分全局作用域（变量）和局部作用域（变量）
        全局作用域（变量）：在任何地方都可以访问的变量
                * 通过关键字var声明的变量
                * 在函数之外通过var声明的变量
                * 没有通过关键字声明的变量并且同时赋值
                
                在函数外部声明的变量
                window对象（拥有全局作用域），window.name，window.top
                
        局部作用域（变量）：在规定的代码块内能够访问的变量
            块级作用域(let拥有的){}：es6 if switch function for  
            `use strict`es6 严格模式 
            
            作用域链：作用域链的存在造成了闭包函数的产生
 ###    十二、闭包函数
       闭包函数： 在函数中存在作用域链，函数中的变量全部保存在作用域链中，这样的特性，我们称为闭包。
      （在函数里面再嵌套一个函数，当我们调用这个函数时就形成了闭包函数）
                        只能子操作父
                      
            闭包函数作用：保存局部变量；
                         在函数外部访问局部变量。
```html
         var a = 10;  全局变量
         function aa(){
             var b = 20;  局部变量
             c = 30;    全局变量
             function bb() {
                 var d = 40;  局部变量
                 console.log(`这是bb`+ a);
                 console.log(`这是bb`+ b);
                 console.log(`这是bb`+ c);
                 console.log(`这是bb`+ d);
             }
             bb();
             console.log(`这是bb`+ a);
             console.log(`这是bb`+ b);
             console.log(`这是bb`+ c);
             d 是bb 的局部变量 是一个闭包函数 所以在bb外输不出d
         }
         console.log(`这是aa`+ a);
         aa()
        b, c, 是aa 的闭包函数所以在外面不能调用
        
        function aa(){
                var a = 10;
                function bb (){
                    return a;
                }
                bb();
                return bb;
            }
            var c = aa();
            console.log(c());
```
###     十三、回调函数
                把一个函数的指针（直接写函数名）
                作为参数传递给另一个函数，这个函数就叫回调函数
                
            传参方式
                1、通过函数的指针
                2、把整个函数传进去

 ### 十四、递归函数
        在函数内部直接调用自己或者间接调用自己

 ### 十五、模拟函数重载
		同一个函数因为传入的参数的类型或个数不同，可以对应多个函数的实现，并且每种实现对应一个函数体

		重载函数常用来实现功能类似而所处理的数据类型不同的问题

### 十六、预解析顺序
	1、按照<script></script>块来解析，有多个<script></script>对时。按块解析，现解析第一个<script></script>中的代码
	2、按环境来解析
	3、遇到关键字var和function时（即以关键字创建的函数），提前解析到内存中（相对应的环境里）。即可在声明前调用
	4、若还有<script></script>，再按照上面的顺序进行解析

### 十七、内置顶层函数
	内置：ECMAScript
	顶层：页面中任何地方都可以调用


	* escape():对字符串进行编码
	对非字母、数字、特殊标点符号（@ + - / * ）的字符串进行编码，最终得到十六进的转义序列，也就是将机器不识别的编码方式编译成机器可以识别的
	
	*  (str):对编码的字符串解释
	有关数据类型转换的
	
	* Number():将任何数据类型转换为数值类型
	如果是布尔值，true为1，false为0；
	如果是数值，转换为本身，会将无意义的后导零于前导零去掉
	如果为null，转换为0；
	如果是undefined，转换为NaN not a number
	如果是字符串：
		如果字符串中只有数字，则转换为数字（十进制）会忽略前导0和后导0
		如果是规范的浮点数，则转换为浮点数会忽略前导0和后导0
		如果为空字符串或者为空，转换为0
		如果是其他值，转换为NaN
	
	* parseInt(23,8)：将任何数据类型转换为整数
	不能写前导零  转换不成功返回NaN
	如果一个字符串中只包含数字，转换为十进制数；
	如果有多个空格（字符串），会先找到第一个非空的值进行转换，直到非数值时结束；
	`如果第一个值不是以数字、空格开头的，一定转换为NaN`
	有两个参数时，第一个参数表示要转换的值第二个参数表示几进制，返回值是十进制的数字；第一个参数从最高位开始计算，只要有一位数可以识别为第二数传入的进制，则可以实现转换，第二个参数可以传入的值为2-36
	
	* parseFloat():将任何数据类型转换为浮点数（小数）并返回
		只有一个点起作用，其它无效
		如果字符串是一个有效的整数，它返回的是整数，不会返回浮点数
		如果第一个值不是以数字空格开头，一定转换为NaN
	
	* string():将任何数据类型转换为字符串
	如果是null，undefined转换为字符串"null" "undefined"
	如果是数值类型，转换为本身的字符串，123转换为“123”；
	如果是布尔类型，true为'true"false为"false"
	
	* Boolean():把任何数据类型转换为布尔型
	转换为假：""(空串)，null，undefined，0，false，NaN
	其他都为真
	
	* isNaN():
	判断一个数据能否转换为数值
	如果能转换为数值返回假，不能返回为真
	
	* eval():
	将符合JS语法规范的字符串转换成JavaScript命令执行（必须在一行）
	
	* toString()；
	将对象以字符串的方式来表示，都是通过对象的方式来调用的
	格式: 对象toString():
		* 数组 分割的字符串
		* 布尔
		* 字符串(还是本身)
		* 数据类型
		* null和undefined没有toString的方法

 ## 对象

### 一、对象：一切皆对象。
        对象指的就是人们所能接触到的所有的事物，有抽象的，也有具体的。
        对象是属性和行为的集合。
          属性：描述对象特征的数据
          行为：操作对象方法的数据
    
        类：具有相同属性和行为的对象的抽象。
            类是对象的抽象；
            对象是类的实例化；

### 二、声明一个对象
        1、实例化
            var Person = new Object();
                var lisi = new Object();
                lisi.name = '李四';
                lisi.age = 23;
                lisi.sex =  '男';
                lisi.say = function(){
                    alert('会说话');
                }
                lisi.say();
                console.log(lisi);
        2、字面量
            var Person1 ={};
             var zhangsan = {
                name:'zhangsan',
                age:23,
                sex:'男',
                say:function(){
                    alert(1);
                }
            }
   			console.log(zhangsan);
        3、构造函数(实现类) 首字母大写
            function Person（）{
    
            }
             function Person（）{
                this.name = name;
                this.age = age;
                this.say = function(){
                    alert('会说话');
                }
            }
            var wangwu = new Person();
    
            var lisi = new Person（）;

### 三、添加属性、方法
    属性：对象.属性名 = 属性值
            对象[`属性名`] = 属性值
    方法：对象.方法名 = function（）{}### 八、对象封装
    		将对象的所有组成部分全部组合起来，并对部分细节进行隐蔽，使其受到保护，只留下和外界的接口
            对象.[`方法名`] = function（）{}

### 四、访问属性、方法
        属性：对象.属性名        
                对象.[`属性名`]
        方法：对象.方法名（）
                对象.[`方法名`]（）

### 五、删除属性、方法
        delete
        delete lili

### 六、清空对象
        null
        lili = null

### 七、for in
        对象：i-> 属性名/方法名
                对象名[i] -> 属性值/方法
        数组：i -> 下标
               对象名[i]  ->   数组的某个数组               

### 八、对象封装
		将对象的所有组成部分全部组合起来，并对部分细节进行隐蔽，使其受到保护，只留下和外界的接口

	1、工厂函数:不推荐。方便维护，节省内存。但是代码不规范
		function myPhone(color){
		var my = {}	;
		my.size = 375;
		my.say= function(){
			alert('打电话');
		}
		return my;
	}
	var iphone1 = myPhone();
	console.log (iphone1.size);

	function myPhone(color){
		var color = color;
		myPhone.size = 375;
		myPhone.cai = `塑料`;
		myPhone.say = function(){
			alert('打电话');
		}
		return myPhone;
	}
	var iphone2 = myPhone();
	console.log(iphone2.size);

	2、构造函数:造成内存浪费
		function Animal(name,age){
	        this.name = name;
	        this.age = age;
	        this.say = function(){
	            alert('会说话');
	        }
	        this.fly = function(){
	        	alert('会飞');
	        }
	    }
	    var green1 = new Animal;
	    console.log(green1);

	    function Ani(name,age){
	    	this.name = name;
	        this.age = age;
	    }
	    Ani.prototype = {
	    	say:function(){
	            alert('会说话');
	        },
	        fly:function(){
	        	alert('会飞');
	        }
	    } 
	    var green1 = new Ani;
	    console.log(green1);

    3、原型 
    	原型：原型也是一个对象。在JS中，每一个对象都会继承另一个对象所有的属性和方法，被继承的对象就是原型。
    	1. 对象：[[prototype]]
    		[[prototype]]是对象内部的一个属性，但是我们不能直接访问。FF和Chrome提供了'poto'访问器，ECM提供了Object.getprototype（object）访问器。指向该对象的原型
    	2. 函数：prototype 保存的是该函数的原型对象



    	3. 原型对象：constructor  指向的是实例的构造函数
		函数对象和原型对象通过prototype和 constructor实现相互关联
		通过prototype可以实现代码共享；实现继承

    		当一个函数作为构造函数来使用时，会把该函数的prototype属性作为原型值赋值给所有通过该构造函数实例化的对象的原型。
    	function Person(name,age){
		this.name = name;
		this.age = age;
		this.say = function(){
            alert('会说话');
        }
		}
		var lisi = new Person;
		console.log(lisi);	
		console.log(lisi.__proto__);
		console.log(Person.prototype);
		
		console.log(Person.prototype === lisi.__proto__);
		console.log(Function.prototype)

    
    4、构造函数结合原型
    	构造函数中一般放属性
    	原型中一般放方法        






