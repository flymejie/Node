# [Py西游攻关之模块](https://www.cnblogs.com/yuanchenqi/articles/5732581.html)

### 模块&包(* * * * *)

#### 模块(modue)的概念：

在计算机程序的开发过程中，随着程序代码越写越多，在一个文件里代码就会越来越长，越来越不容易维护。

为了编写可维护的代码，我们把很多函数分组，分别放到不同的文件里，这样，每个文件包含的代码就相对较少，很多编程语言都采用这种组织代码的方式。在Python中，一个.py文件就称之为一个模块（Module）。

使用模块有什么好处？

最大的好处是大大提高了代码的可维护性。

其次，编写代码不必从零开始。当一个模块编写完毕，就可以被其他地方引用。我们在编写程序的时候，也经常引用其他模块，包括Python内置的模块和来自第三方的模块。

所以，模块一共三种：

- python标准库
- 第三方模块
- 应用程序自定义模块

另外，使用模块还可以避免函数名和变量名冲突。相同名字的函数和变量完全可以分别存在不同的模块中，因此，我们自己在编写模块时，不必考虑名字会与其他模块冲突。但是也要注意，尽量不要与内置函数名字冲突。

#### 模块导入方法

**1 import 语句**

```
`import` `module1[, module2[,... moduleN]`
```

当我们使用import语句的时候，Python解释器是怎样找到对应的文件的呢？答案就是解释器有自己的搜索路径，存在sys.path里。　　

```
`['``', '``/``usr``/``lib``/``python3.``4``', '``/``usr``/``lib``/``python3.``4``/``plat``-``x86_64``-``linux``-``gnu',``'/usr/lib/python3.4/lib-dynload'``, ``'/usr/local/lib/python3.4/dist-packages'``, ``'/usr/lib/python3/dist-packages'``]　　`
```

因此若像我一样在当前目录下存在与要引入模块同名的文件，就会把要引入的模块屏蔽掉。

**2  from…import 语句**

```
`from` `modname ``import` `name1[, name2[, ... nameN]]`
```

这个声明不会把整个modulename模块导入到当前的命名空间中，只会将它里面的name1或name2单个引入到执行这个声明的模块的全局符号表。

**3  From…import\* 语句**

```
`from` `modname ``import` `*`
```

这提供了一个简单的方法来导入一个模块中的所有项目。然而这种声明不该被过多地使用。大多数情况， Python程序员不使用这种方法，因为引入的其它来源的命名，很可能覆盖了已有的定义。

**4 运行本质**　

```
`#1 import test``#2 from test import add　　`
```

无论1还是2，首先通过sys.path找到test.py,然后执行test脚本（全部执行），区别是1会将test这个变量名加载到名字空间，而2只会将add这个变量名加载进来。　　

#### 包(package)

如果不同的人编写的模块名相同怎么办？为了避免模块名冲突，Python又引入了按目录来组织模块的方法，称为包（Package）。

举个例子，一个`abc.py`的文件就是一个名字叫`abc`的模块，一个`xyz.py`的文件就是一个名字叫`xyz`的模块。

现在，假设我们的`abc`和`xyz`这两个模块名字与其他模块冲突了，于是我们可以通过包来组织模块，避免冲突。方法是选择一个顶层包名：

​             ![img](https://images2015.cnblogs.com/blog/877318/201609/877318-20160913071822680-1730797664.png)         

引入了包以后，只要顶层的包名不与别人冲突，那所有模块都不会与别人冲突。现在，`view.py`模块的名字就变成了hello_django.app01`.views`，类似的，manage`.py`的模块名则是hello_django.manage。

请注意，每一个包目录下面都会有一个`__init__.py`的文件，这个文件是必须存在的，否则，Python就把这个目录当成普通目录(文件夹)，而不是一个包。`__init__.py`可以是空文件，也可以有Python代码，因为`__init__.py`本身就是一个模块，而它的模块名就是对应包的名字。

调用包就是执行包下的__init__.py文件

####  注意点（important）

![img](https://images2015.cnblogs.com/blog/877318/201609/877318-20160913072617289-1787847933.png)

1--------------

在nod1里import  hello是找不到的，有同学说可以找到呀，那是因为你的pycharm为你把myapp这一层路径加入到了sys.path里面，所以可以找到，然而程序一旦在命令行运行，则报错。有同学问那怎么办？简单啊，自己把这个路径加进去不就OK啦：

```
`import` `sys,os``BASE_DIR``=``os.path.dirname(os.path.dirname(os.path.abspath(__file__)))``sys.path.append(BASE_DIR)``import` `hello``hello.hello1()`
```

2 --------------

```
`if` `__name__``=``=``'__main__'``:``  ``print``(``'ok'``)`
```

**“Make a .py both importable and executable”**

   如果我们是直接执行某个.py文件的时候，该文件中那么”__name__ == '__main__'“是True,但是我们如果从另外一个.py文件通过import导入该文件的时候，这时__name__的值就是我们这个py文件的名字而不是__main__。

   这个功能还有一个用处：调试代码的时候，在”if __name__ == '__main__'“中加入一些我们的调试代码，我们可以让外部模块调用的时候不执行我们的调试代码，但是如果我们想排查问题的时候，直接执行该模块文件，调试代码能够正常运行！s

3 　　

![img](https://images2015.cnblogs.com/blog/877318/201609/877318-20160913143701633-1174796480.png)

```
`##-------------cal.py``def` `add(x,y):` `  ``return` `x``+``y``##-------------main.py``import` `cal   ``#from module import cal` `def` `main():` `  ``cal.add(``1``,``2``)``  ` `##--------------bin.py``from` `module ``import` `main` `main.main()`
```

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) 注意

### time模块(* * * *)

#### 三种时间表示

在Python中，通常有这几种方式来表示时间：

- 时间戳(timestamp) ：     通常来说，时间戳表示的是从1970年1月1日00:00:00开始按秒计算的偏移量。我们运行“type(time.time())”，返回的是float类型。
- 格式化的时间字符串
- 元组(struct_time)  ：     struct_time元组共有9个元素共九个元素:(年，月，日，时，分，秒，一年中第几周，一年中第几天，夏令时)

```
`import` `time` `# 1 time() :返回当前时间的时间戳``time.time() ``#1473525444.037215` `#----------------------------------------------------------` `# 2 localtime([secs])``# 将一个时间戳转换为当前时区的struct_time。secs参数未提供，则以当前时间为准。``time.localtime() ``#time.struct_time(tm_year=2016, tm_mon=9, tm_mday=11, tm_hour=0,``# tm_min=38, tm_sec=39, tm_wday=6, tm_yday=255, tm_isdst=0)``time.localtime(``1473525444.037215``)` `#----------------------------------------------------------` `# 3 gmtime([secs]) 和localtime()方法类似，gmtime()方法是将一个时间戳转换为UTC时区（0时区）的struct_time。` `#----------------------------------------------------------` `# 4 mktime(t) : 将一个struct_time转化为时间戳。``print``(time.mktime(time.localtime()))``#1473525749.0` `#----------------------------------------------------------` `# 5 asctime([t]) : 把一个表示时间的元组或者struct_time表示为这种形式：'Sun Jun 20 23:21:05 1993'。``# 如果没有参数，将会将time.localtime()作为参数传入。``print``(time.asctime())``#Sun Sep 11 00:43:43 2016` `#----------------------------------------------------------` `# 6 ctime([secs]) : 把一个时间戳（按秒计算的浮点数）转化为time.asctime()的形式。如果参数未给或者为``# None的时候，将会默认time.time()为参数。它的作用相当于time.asctime(time.localtime(secs))。``print``(time.ctime()) ``# Sun Sep 11 00:46:38 2016` `print``(time.ctime(time.time())) ``# Sun Sep 11 00:46:38 2016` `# 7 strftime(format[, t]) : 把一个代表时间的元组或者struct_time（如由time.localtime()和``# time.gmtime()返回）转化为格式化的时间字符串。如果t未指定，将传入time.localtime()。如果元组中任何一个``# 元素越界，ValueError的错误将会被抛出。``print``(time.strftime(``"%Y-%m-%d %X"``, time.localtime()))``#2016-09-11 00:49:56` `# 8 time.strptime(string[, format])``# 把一个格式化时间字符串转化为struct_time。实际上它和strftime()是逆操作。``print``(time.strptime(``'2011-05-05 16:37:06'``, ``'%Y-%m-%d %X'``))` `#time.struct_time(tm_year=2011, tm_mon=5, tm_mday=5, tm_hour=16, tm_min=37, tm_sec=6,``# tm_wday=3, tm_yday=125, tm_isdst=-1)` `#在这个函数中，format默认为："%a %b %d %H:%M:%S %Y"。` `# 9 sleep(secs)``# 线程推迟指定的时间运行，单位为秒。` `# 10 clock()``# 这个需要注意，在不同的系统上含义不同。在UNIX系统上，它返回的是“进程时间”，它是用秒表示的浮点数（时间戳）。``# 而在WINDOWS中，第一次调用，返回的是进程运行的实际时间。而第二次之后的调用是自第一次调用以后到现在的运行``# 时间，即两次时间差。`
```

​       ![img](https://images2015.cnblogs.com/blog/877318/201609/877318-20160911074627840-300139608.png)![img](https://images2015.cnblogs.com/blog/877318/201609/877318-20160911074646389-1201523256.png)

```
`help``(time)``help``(time.asctime)`
```

### random模块(* *)

```
`import` `random` `print``(random.random())``#(0,1)----float` `print``(random.randint(``1``,``3``)) ``#[1,3]` `print``(random.randrange(``1``,``3``)) ``#[1,3)` `print``(random.choice([``1``,``'23'``,[``4``,``5``]]))``#23` `print``(random.sample([``1``,``'23'``,[``4``,``5``]],``2``))``#[[4, 5], '23']` `print``(random.uniform(``1``,``3``))``#1.927109612082716` `item``=``[``1``,``3``,``5``,``7``,``9``]``random.shuffle(item)``print``(item)`
```

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) 验证码

###  os模块(* * * *)

os模块是与操作系统交互的一个接口

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) View Code

### sys模块(* * *)

```
`sys.argv      命令行参数``List``，第一个元素是程序本身路径``sys.exit(n)    退出程序，正常退出时exit(``0``)``sys.version    获取Python解释程序的版本信息``sys.maxint     最大的``Int``值``sys.path      返回模块的搜索路径，初始化时使用PYTHONPATH环境变量的值``sys.platform    返回操作系统平台名称`
```

**进度条：**

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) View Code

### json & pickle(* * * *)

之前我们学习过用eval内置方法可以将一个字符串转成python对象，不过，eval方法是有局限性的，对于普通的数据类型，json.loads和eval都能用，但遇到特殊类型的时候，eval就不管用了,所以eval的重点还是通常用来执行一个字符串表达式，并返回表达式的值。

```
`import` `json``x``=``"[null,true,false,1]"``print``(``eval``(x))``print``(json.loads(x))`
```

#### 什么是序列化？

我们把对象(变量)从内存中变成可存储或传输的过程称之为序列化，在Python中叫pickling，在其他语言中也被称之为serialization，marshalling，flattening等等，都是一个意思。

序列化之后，就可以把序列化后的内容写入磁盘，或者通过网络传输到别的机器上。

反过来，把变量内容从序列化的对象重新读到内存里称之为反序列化，即unpickling。

#### json

如果我们要在不同的编程语言之间传递对象，就必须把对象序列化为标准格式，比如XML，但更好的方法是序列化为JSON，因为JSON表示出来就是一个字符串，可以被所有语言读取，也可以方便地存储到磁盘或者通过网络传输。JSON不仅是标准格式，并且比XML更快，而且可以直接在Web页面中读取，非常方便。

JSON表示的对象就是标准的JavaScript语言的对象，JSON和Python内置的数据类型对应如下：

![img](https://images2015.cnblogs.com/blog/877318/201609/877318-20160911105642628-530508765.png)

```
`#----------------------------序列化``import` `json` `dic``=``{``'name'``:``'alvin'``,``'age'``:``23``,``'sex'``:``'male'``}``print``(``type``(dic))``#` `j``=``json.dumps(dic)``print``(``type``(j))``#` `f``=``open``(``'序列化对象'``,``'w'``)``f.write(j) ``#-------------------等价于json.dump(dic,f)``f.close()``#-----------------------------反序列化 ``import` `json``f``=``open``(``'序列化对象'``)``data``=``json.loads(f.read())``# 等价于data=json.load(f)`
```

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) 注意点

#### pickle　

```
`##----------------------------序列化``import` `pickle` `dic``=``{``'name'``:``'alvin'``,``'age'``:``23``,``'sex'``:``'male'``}` `print``(``type``(dic))``#` `j``=``pickle.dumps(dic)``print``(``type``(j))``#` `f``=``open``(``'序列化对象_pickle'``,``'wb'``)``#注意是w是写入str,wb是写入bytes,j是'bytes'``f.write(j) ``#-------------------等价于pickle.dump(dic,f)` `f.close()``#-------------------------反序列化``import` `pickle``f``=``open``(``'序列化对象_pickle'``,``'rb'``)` `data``=``pickle.loads(f.read())``# 等价于data=pickle.load(f)` `print``(data[``'age'``])  `
```

   Pickle的问题和所有其他编程语言特有的序列化问题一样，就是它只能用于Python，并且可能不同版本的Python彼此都不兼容，因此，只能用Pickle保存那些不重要的数据，不能成功地反序列化也没关系。

### shelve模块(* * *)

 shelve模块比pickle模块简单，只有一个open函数，返回类似字典的对象，可读可写;key必须为字符串，而值可以是python所支持的数据类型

```
`import` `shelve` `f ``=` `shelve.``open``(r``'shelve.txt'``)` `# f['stu1_info']={'name':'alex','age':'18'}``# f['stu2_info']={'name':'alvin','age':'20'}``# f['school_info']={'website':'oldboyedu.com','city':'beijing'}``#``#``# f.close()` `print``(f.get(``'stu_info'``)[``'age'``])`
```

### xml模块(* *)

xml是实现不同语言或程序之间进行数据交换的协议，跟json差不多，但json使用起来更简单，不过，古时候，在json还没诞生的黑暗年代，大家只能选择用xml呀，至今很多传统公司如金融行业的很多系统的接口还主要是xml。

xml的格式如下，就是通过<>节点来区别数据结构的:

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) xml数据

xml协议在各个语言里的都 是支持的，在python中可以用以下模块操作xml：

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) View Code

自己创建xml文档：

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) 创建xml文档

### **configparser模块(\* \*)**

**来看一个好多软件的常见文档格式如下：**

```
`[DEFAULT]``ServerAliveInterval ``=` `45``Compression ``=` `yes``CompressionLevel ``=` `9``ForwardX11 ``=` `yes`` ` `[bitbucket.org]``User ``=` `hg`` ` `[topsecret.server.com]``Port ``=` `50022``ForwardX11 ``=` `no`
```

如果想用python生成一个这样的文档怎么做呢？

```
`import` `configparser`` ` `config ``=` `configparser.ConfigParser()``config[``"DEFAULT"``] ``=` `{``'ServerAliveInterval'``: ``'45'``,``           ``'Compression'``: ``'yes'``,``           ``'CompressionLevel'``: ``'9'``}`` ` `config[``'bitbucket.org'``] ``=` `{}``config[``'bitbucket.org'``][``'User'``] ``=` `'hg'``config[``'topsecret.server.com'``] ``=` `{}``topsecret ``=` `config[``'topsecret.server.com'``]``topsecret[``'Host Port'``] ``=` `'50022'`   `# mutates the parser``topsecret[``'ForwardX11'``] ``=` `'no'` `# same here``config[``'DEFAULT'``][``'ForwardX11'``] ``=` `'yes'`` ``with ``open``(``'example.ini'``, ``'w'``) as configfile:``  ``config.write(configfile)`
```

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) 增删改查

### **hashlib模块(\* \*)**

用于加密相关的操作，3.x里代替了md5模块和sha模块，主要提供 SHA1, SHA224, SHA256, SHA384, SHA512 ，MD5 算法

```
`import` `hashlib` `m``=``hashlib.md5()``# m=hashlib.sha256()` `m.update(``'hello'``.encode(``'utf8'``))``print``(m.hexdigest()) ``#5d41402abc4b2a76b9719d911017c592` `m.update(``'alvin'``.encode(``'utf8'``))` `print``(m.hexdigest()) ``#92a7e713c30abbb0319fa07da2a5c4af` `m2``=``hashlib.md5()``m2.update(``'helloalvin'``.encode(``'utf8'``))``print``(m2.hexdigest()) ``#92a7e713c30abbb0319fa07da2a5c4af`
```

以上加密算法虽然依然非常厉害，但时候存在缺陷，即：通过撞库可以反解。所以，有必要对加密算法中添加自定义key再来做加密。

```
`import` `hashlib` `# ######## 256 ########` `hash` `=` `hashlib.sha256(``'898oaFs09f'``.encode(``'utf8'``))``hash``.update(``'alvin'``.encode(``'utf8'``))``print` `(``hash``.hexdigest())``#e79e68f070cdedcfe63eaf1a2e92c83b4cfb1b5c6bc452d214c1b7e77cdfd1c7`
```

python 还有一个 hmac 模块，它内部对我们创建 key 和 内容 再进行处理然后再加密:

```
`import` `hmac``h ``=` `hmac.new(``'alvin'``.encode(``'utf8'``))``h.update(``'hello'``.encode(``'utf8'``))``print` `(h.hexdigest())``#320df9832eab4c038b6c1d7ed73a5940`
```

### subprocess模块(* * * *)

   当我们需要调用系统的命令的时候，最先考虑的os模块。用os.system()和os.popen()来进行操作。但是这两个命令过于简单，不能完成一些复杂的操作，如给运行的命令提供输入或者读取命令的输出，判断该命令的运行状态，管理多个命令的并行等等。这时subprocess中的Popen命令就能有效的完成我们需要的操作。

   subprocess模块允许一个进程创建一个新的子进程，通过管道连接到子进程的stdin/stdout/stderr，获取子进程的返回值等操作。 

The subprocess module allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.

This module intends to replace several other, older modules and functions, such as: os.system、os.spawn*、os.popen*、popen2.*、commands.*

 

这个模块一个类：Popen。

```
`#Popen它的构造函数如下：` `subprocess.Popen(args, bufsize``=``0``, executable``=``None``, stdin``=``None``, stdout``=``None``,stderr``=``None``, preexec_fn``=``None``, close_fds``=``False``, shell``=``False``,          cwd``=``None``, env``=``None``, universal_newlines``=``False``, startupinfo``=``None``, creationflags``=``0``)`
```

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) parameter

#### 简单命令：

```
`import` `subprocess` `a``=``subprocess.Popen(``'ls'``)``# 创建一个新的进程,与主进程不同步` `print``(``'>>>>>>>'``,a)``#a是Popen的一个实例对象` `'''``>>>>>>> ``__init__.py``__pycache__``log.py``main.py` `'''` `# subprocess.Popen('ls -l',shell=True)` `# subprocess.Popen(['ls','-l'])`
```

#### subprocess.PIPE

在创建Popen对象时，subprocess.PIPE可以初始化stdin, stdout或stderr参数。表示与子进程通信的标准流。

```
`import` `subprocess` `# subprocess.Popen('ls')``p``=``subprocess.Popen(``'ls'``,stdout``=``subprocess.PIPE)``#结果跑哪去啦?` `print``(p.stdout.read())``#这这呢:b'__pycache__\nhello.py\nok.py\nweb\n'`
```

这是因为subprocess创建了子进程，结果本在子进程中，if 想要执行结果转到主进程中，就得需要一个管道，即 ： stdout=subprocess.PIPE

#### subprocess.STDOUT

创建Popen对象时，用于初始化stderr参数，表示将错误通过标准输出流输出。

#### Popen的方法

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) View Code

#### supprocess模块的工具函数

```
`supprocess模块提供了一些函数，方便我们用于创建进程来实现一些简单的功能。` `subprocess.call(``*``popenargs, ``*``*``kwargs)``运行命令。该函数将一直等待到子进程运行结束，并返回进程的returncode。如果子进程不需要进行交 互,就可以使用该函数来创建。` `subprocess.check_call(``*``popenargs, ``*``*``kwargs)``与subprocess.call(``*``popenargs, ``*``*``kwargs)功能一样，只是如果子进程返回的returncode不为``0``的话，将触发CalledProcessError异常。在异常对象中，包 括进程的returncode信息。` `check_output(``*``popenargs, ``*``*``kwargs)``与call()方法类似，以byte string的方式返回子进程的输出，如果子进程的返回值不是``0``，它抛出CalledProcessError异常，这个异常中的returncode包含返回码，output属性包含已有的输出。` `getstatusoutput(cmd)``/``getoutput(cmd)``这两个函数仅仅在Unix下可用，它们在shell中执行指定的命令cmd，前者返回(status, output)，后者返回output。其中，这里的output包括子进程的stdout和stderr。`
```

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) 演示

####  交互命令：

终端输入的命令分为两种：

- 输入即可得到输出，如：ifconfig
- 输入进行某环境，依赖再输入，如：python

需要交互的命令示例

待续

### logging模块(* * * * *)

一 (简单应用)

```
import logging  
logging.debug('debug message')  
logging.info('info message')  
logging.warning('warning message')  
logging.error('error message')  
logging.critical('critical message')  
```

输出：

WARNING:root:warning message
ERROR:root:error message
CRITICAL:root:critical message

可见，默认情况下[Python](http://lib.csdn.net/base/11)的logging模块将日志打印到了标准输出中，且只显示了大于等于WARNING级别的日志，这说明默认的日志级别设置为WARNING（日志级别等级CRITICAL > ERROR > WARNING > INFO > DEBUG > NOTSET），默认的日志格式为日志级别：Logger名称：用户输出消息。

 

二  **灵活配置日志级别，日志格式，输出位置**

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import logging  
logging.basicConfig(level=logging.DEBUG,  
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',  
                    datefmt='%a, %d %b %Y %H:%M:%S',  
                    filename='/tmp/test.log',  
                    filemode='w')  
  
logging.debug('debug message')  
logging.info('info message')  
logging.warning('warning message')  
logging.error('error message')  
logging.critical('critical message')
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

查看输出：
cat /tmp/test.log 
Mon, 05 May 2014 16:29:53 test_logging.py[line:9] DEBUG debug message
Mon, 05 May 2014 16:29:53 test_logging.py[line:10] INFO info message
Mon, 05 May 2014 16:29:53 test_logging.py[line:11] WARNING warning message
Mon, 05 May 2014 16:29:53 test_logging.py[line:12] ERROR error message
Mon, 05 May 2014 16:29:53 test_logging.py[line:13] CRITICAL critical message

可见在logging.basicConfig()函数中可通过具体参数来更改logging模块默认行为，可用参数有
filename：用指定的文件名创建FiledHandler（后边会具体讲解handler的概念），这样日志会被存储在指定的文件中。
filemode：文件打开方式，在指定了filename时使用这个参数，默认值为“a”还可指定为“w”。
format：指定handler使用的日志显示格式。
datefmt：指定日期时间格式。
level：设置rootlogger（后边会讲解具体概念）的日志级别
stream：用指定的stream创建StreamHandler。可以指定输出到sys.stderr,sys.stdout或者文件(f=open('test.log','w'))，默认为sys.stderr。若同时列出了filename和stream两个参数，则stream参数会被忽略。

format参数中可能用到的格式化串：
%(name)s Logger的名字
%(levelno)s 数字形式的日志级别
%(levelname)s 文本形式的日志级别
%(pathname)s 调用日志输出函数的模块的完整路径名，可能没有
%(filename)s 调用日志输出函数的模块的文件名
%(module)s 调用日志输出函数的模块名
%(funcName)s 调用日志输出函数的函数名
%(lineno)d 调用日志输出函数的语句所在的代码行
%(created)f 当前时间，用UNIX标准的表示时间的浮 点数表示
%(relativeCreated)d 输出日志信息时的，自Logger创建以 来的毫秒数
%(asctime)s 字符串形式的当前时间。默认格式是 “2003-07-08 16:49:45,896”。逗号后面的是毫秒
%(thread)d 线程ID。可能没有
%(threadName)s 线程名。可能没有
%(process)d 进程ID。可能没有
%(message)s用户输出的消息

 

三  logger对象

  上述几个例子中我们了解到了logging.debug()、logging.info()、logging.warning()、logging.error()、logging.critical()（分别用以记录不同级别的日志信息），logging.basicConfig()（用默认日志格式（Formatter）为日志系统建立一个默认的流处理器（StreamHandler），设置基础配置（如日志级别等）并加到root logger（根Logger）中）这几个logging模块级别的函数，另外还有一个模块级别的函数是logging.getLogger([name])（返回一个logger对象，如果没有指定名字将返回root logger）

   先看一个最简单的过程：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
import logging

logger = logging.getLogger()
# 创建一个handler，用于写入日志文件
fh = logging.FileHandler('test.log')

# 再创建一个handler，用于输出到控制台
ch = logging.StreamHandler()

formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

fh.setFormatter(formatter)
ch.setFormatter(formatter)

logger.addHandler(fh) #logger对象可以添加多个fh和ch对象
logger.addHandler(ch)

logger.debug('logger debug message')
logger.info('logger info message')
logger.warning('logger warning message')
logger.error('logger error message')
logger.critical('logger critical message')
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

   先简单介绍一下，logging库提供了多个组件：Logger、Handler、Filter、Formatter。Logger对象提供应用程序可直接使用的接口，Handler发送日志到适当的目的地，Filter提供了过滤日志信息的方法，Formatter指定日志显示格式。

   (1)

   Logger是一个树形层级结构，输出信息之前都要获得一个Logger（如果没有显示的获取则自动创建并使用root Logger，如第一个例子所示）。
   logger = logging.getLogger()返回一个默认的Logger也即root Logger，并应用默认的日志级别、Handler和Formatter设置。
当然也可以通过Logger.setLevel(lel)指定最低的日志级别，可用的日志级别有logging.DEBUG、logging.INFO、logging.WARNING、logging.ERROR、logging.CRITICAL。
   Logger.debug()、Logger.info()、Logger.warning()、Logger.error()、Logger.critical()输出不同级别的日志，只有日志等级大于或等于设置的日志级别的日志才会被输出。 

```
logger.debug('logger debug message')  
logger.info('logger info message')  
logger.warning('logger warning message')  
logger.error('logger error message')  
logger.critical('logger critical message')  
```

只输出了
2014-05-06 12:54:43,222 - root - WARNING - logger warning message
2014-05-06 12:54:43,223 - root - ERROR - logger error message
2014-05-06 12:54:43,224 - root - CRITICAL - logger critical message
   从这个输出可以看出logger = logging.getLogger()返回的Logger名为root。这里没有用logger.setLevel(logging.Debug)显示的为logger设置日志级别，所以使用默认的日志级别WARNIING，故结果只输出了大于等于WARNIING级别的信息。

   (2) 如果我们再创建两个logger对象： 

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
##################################################
logger1 = logging.getLogger('mylogger')
logger1.setLevel(logging.DEBUG)

logger2 = logging.getLogger('mylogger')
logger2.setLevel(logging.INFO)

logger1.addHandler(fh)
logger1.addHandler(ch)

logger2.addHandler(fh)
logger2.addHandler(ch)

logger1.debug('logger1 debug message')
logger1.info('logger1 info message')
logger1.warning('logger1 warning message')
logger1.error('logger1 error message')
logger1.critical('logger1 critical message')
  
logger2.debug('logger2 debug message')
logger2.info('logger2 info message')
logger2.warning('logger2 warning message')
logger2.error('logger2 error message')
logger2.critical('logger2 critical message')
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

结果：

   ![img](https://images2015.cnblogs.com/blog/877318/201608/877318-20160803130723622-772276541.png)

这里有两个个问题：

   <1>我们明明通过logger1.setLevel(logging.DEBUG)将logger1的日志级别设置为了DEBUG，为何显示的时候没有显示出DEBUG级别的日志信息，而是从INFO级别的日志开始显示呢？

​    原来logger1和logger2对应的是同一个Logger实例，只要logging.getLogger（name）中名称参数name相同则返回的Logger实例就是同一个，且仅有一个，也即name与Logger实例一一对应。在logger2实例中通过logger2.setLevel(logging.INFO)设置mylogger的日志级别为logging.INFO，所以最后logger1的输出遵从了后来设置的日志级别。

   <2>为什么logger1、logger2对应的每个输出分别显示两次?
    这是因为我们通过logger = logging.getLogger()显示的创建了root Logger，而logger1 = logging.getLogger('mylogger')创建了root Logger的孩子(root.)mylogger,logger2同样。而孩子,孙子，重孙……既会将消息分发给他的handler进行处理也会传递给所有的祖先Logger处理。

​    ok,那么现在我们把

\# logger.addHandler(fh)

\# logger.addHandler(ch)  注释掉，我们再来看效果：

 *![img](https://images2015.cnblogs.com/blog/877318/201608/877318-20160803131623028-674109084.png)*

*因为我们注释了logger对象显示的位置，所以才用了默认方式，即标准输出方式。*因为它的父级没有设置文件显示方式，所以在这里只打印了一次。

孩子,孙子，重孙……可逐层继承来自祖先的日志级别、Handler、Filter设置，也可以通过Logger.setLevel(lel)、Logger.addHandler(hdlr)、Logger.removeHandler(hdlr)、Logger.addFilter(filt)、Logger.removeFilter(filt)。设置自己特别的日志级别、Handler、Filter。若不设置则使用继承来的值。

<3>**Filter**
   限制只有满足过滤规则的日志才会输出。
   比如我们定义了filter = logging.Filter('a.b.c'),并将这个Filter添加到了一个Handler上，则使用该Handler的Logger中只有名字带      a.b.c前缀的Logger才能输出其日志。

 

   filter = logging.Filter('mylogger') 

   logger.addFilter(filter)

   这是只对logger这个对象进行筛选

   如果想对所有的对象进行筛选，则：

   filter = logging.Filter('mylogger') 

   fh.addFilter(filter)

   ch.addFilter(filter)

   *这样，所有添加fh或者ch的logger对象都会进行筛选。*

*完整代码1：*

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) View Code

​    *完整代码2：*

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) View Code

应用：   

![img](https://images.cnblogs.com/OutliningIndicators/ContractedBlock.gif) View Code

###  re模块(* * * * *)

就其本质而言，正则表达式（或 RE）是一种小型的、高度专业化的编程语言，（在Python中）它内嵌在Python中，并通过 re 模块实现。正则表达式模式被编译成一系列的字节码，然后由用 C 编写的匹配引擎执行。

字符匹配（普通字符，元字符）：

1 普通字符：大多数字符和字母都会和自身匹配
       \>>> re.findall('alvin','yuanaleSxalexwupeiqi')
           ['alvin'] 

2 元字符：. ^ $ * + ? { } [ ] | ( ) \

#### 元字符之. ^ $ * + ? { }

```
`import` `re` `ret``=``re.findall(``'a..in'``,``'helloalvin'``)``print``(ret)``#['alvin']` `ret``=``re.findall(``'^a...n'``,``'alvinhelloawwwn'``)``print``(ret)``#['alvin']` `ret``=``re.findall(``'a...n$'``,``'alvinhelloawwwn'``)``print``(ret)``#['awwwn']` `ret``=``re.findall(``'a...n$'``,``'alvinhelloawwwn'``)``print``(ret)``#['awwwn']` `ret``=``re.findall(``'abc*'``,``'abcccc'``)``#贪婪匹配[0,+oo] ``print``(ret)``#['abcccc']` `ret``=``re.findall(``'abc+'``,``'abccc'``)``#[1,+oo]``print``(ret)``#['abccc']` `ret``=``re.findall(``'abc?'``,``'abccc'``)``#[0,1]``print``(ret)``#['abc']` `ret``=``re.findall(``'abc{1,4}'``,``'abccc'``)``print``(ret)``#['abccc'] 贪婪匹配`
```

注意：前面的*,+,?等都是贪婪匹配，也就是尽可能匹配，后面加?号使其变成惰性匹配

```
`ret``=``re.findall(``'abc*?'``,``'abcccccc'``)``print``(ret)``#['ab']`
```

#### 元字符之字符集［］：

```
`#--------------------------------------------字符集[]``ret``=``re.findall(``'a[bc]d'``,``'acd'``)``print``(ret)``#['acd']` `ret``=``re.findall(``'[a-z]'``,``'acd'``)``print``(ret)``#['a', 'c', 'd']` `ret``=``re.findall(``'[.*+]'``,``'a.cd+'``)``print``(ret)``#['.', '+']` `#在字符集里有功能的符号: - ^ \` `ret``=``re.findall(``'[1-9]'``,``'45dha3'``)``print``(ret)``#['4', '5', '3']` `ret``=``re.findall(``'[^ab]'``,``'45bdha3'``)``print``(ret)``#['4', '5', 'd', 'h', '3']` `ret``=``re.findall(``'[\d]'``,``'45bdha3'``)``print``(ret)``#['4', '5', '3']`
```

#### 元字符之转义符\

反斜杠后边跟元字符去除特殊功能,比如\.
反斜杠后边跟普通字符实现特殊功能,比如\d

\d  匹配任何十进制数；它相当于类 [0-9]。
\D 匹配任何非数字字符；它相当于类 [^0-9]。
\s  匹配任何空白字符；它相当于类 [ \t\n\r\f\v]。
\S 匹配任何非空白字符；它相当于类 [^ \t\n\r\f\v]。
\w 匹配任何字母数字字符；它相当于类 [a-zA-Z0-9_]。
\W 匹配任何非字母数字字符；它相当于类 [^a-zA-Z0-9_]
\b  匹配一个特殊字符边界，比如空格 ，&，＃等

```
`ret``=``re.findall(``'I\b'``,``'I am LIST'``)``print``(ret)``#[]``ret``=``re.findall(r``'I\b'``,``'I am LIST'``)``print``(ret)``#['I']`
```

现在我们聊一聊\,先看下面两个匹配：

```
`#-----------------------------eg1:``import` `re``ret``=``re.findall(``'c\l'``,``'abc\le'``)``print``(ret)``#[]``ret``=``re.findall(``'c\\l'``,``'abc\le'``)``print``(ret)``#[]``ret``=``re.findall(``'c\\\\l'``,``'abc\le'``)``print``(ret)``#['c\\l']``ret``=``re.findall(r``'c\\l'``,``'abc\le'``)``print``(ret)``#['c\\l']` `#-----------------------------eg2:``#之所以选择\b是因为\b在ASCII表中是有意义的``m ``=` `re.findall(``'\bblow'``, ``'blow'``)``print``(m)``m ``=` `re.findall(r``'\bblow'``, ``'blow'``)``print``(m)`
```

​           ![img](https://images2015.cnblogs.com/blog/877318/201609/877318-20160911221511963-1888449004.png)　　

#### 元字符之分组()

```
`m ``=` `re.findall(r``'(ad)+'``, ``'add'``)``print``(m)` `ret``=``re.search(``'(?P\d{2})/(?P\w{3})'``,``'23/com'``)``print``(ret.group())``#23/com``print``(ret.group(``'id'``))``#23`
```

#### 元字符之｜

```
`ret``=``re.search(``'(ab)|\d'``,``'rabhdg8sd'``)``print``(ret.group())``#ab`
```

#### re模块下的常用方法

```
`import` `re``#1``re.findall(``'a'``,``'alvin yuan'``)  ``#返回所有满足匹配条件的结果,放在列表里``#2``re.search(``'a'``,``'alvin yuan'``).group() ``#函数会在字符串内查找模式匹配,只到找到第一个匹配然后返回一个包含匹配信息的对象,该对象可以``                   ``# 通过调用group()方法得到匹配的字符串,如果字符串没有匹配，则返回None。` `#3``re.match(``'a'``,``'abc'``).group()   ``#同search,不过尽在字符串开始处进行匹配` `#4``ret``=``re.split(``'[ab]'``,``'abcd'``)   ``#先按'a'分割得到''和'bcd',在对''和'bcd'分别按'b'分割``print``(ret)``#['', '', 'cd']` `#5``ret``=``re.sub(``'\d'``,``'abc'``,``'alvin5yuan6'``,``1``)``print``(ret)``#alvinabcyuan6``ret``=``re.subn(``'\d'``,``'abc'``,``'alvin5yuan6'``)``print``(ret)``#('alvinabcyuanabc', 2)` `#6``obj``=``re.``compile``(``'\d{3}'``)``ret``=``obj.search(``'abc123eeee'``)``print``(ret.group())``#123`
```

注意：

```
`import` `re` `ret``=``re.findall(``'www.(baidu|oldboy).com'``,``'www.oldboy.com'``)``print``(ret)``#['oldboy']   这是因为findall会优先把匹配结果组里内容返回,如果想要匹配结果,取消权限即可` `ret``=``re.findall(``'www.(?:baidu|oldboy).com'``,``'www.oldboy.com'``)``print``(ret)``#['www.oldboy.com']`
```

补充：

![img](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

```
import re

print(re.findall("<(?P<tag_name>\w+)>\w+</(?P=tag_name)>","<h1>hello</h1>"))
print(re.search("<(?P<tag_name>\w+)>\w+</(?P=tag_name)>","<h1>hello</h1>"))
print(re.search(r"<(\w+)>\w+</\1>","<h1>hello</h1>"))
```

补充2

![img](https://images.cnblogs.com/OutliningIndicators/ExpandedBlockStart.gif)

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
#匹配出所有的整数
import re

#ret=re.findall(r"\d+{0}]","1-2*(60+(-40.35/5)-(-4*3))")
ret=re.findall(r"-?\d+\.\d*|(-?\d+)","1-2*(60+(-40.35/5)-(-4*3))")
ret.remove("")

print(ret)
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

　　