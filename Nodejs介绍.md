# Nodejs介绍

## 介绍
	Nodejs是一个JavaScript的运行环境，它让JavaScript可以开发后端程序，实现几乎其它后台语言实现的所有功能(PHP JSP Pthon)


## 优势
	1.Nodejs语法完全是JS语法，
	2.Nodejs超强的高并发能力 非阻塞
	3.实现高性能服务器
	4.开发周期短，开发成本低，学习成本低

### 回调函数解决异步非阻塞无数据的问题

```javascript
let fs = require('fs');
function getMime(callback){
    fs.readFile('../http/mime.json',function(err,data){
        callback(data);
    });
}
let data = getMime(function(data){
    console.log(data.toString());
});

__dirname  当前文件目录
```



## Nodejs适合做什么

## Nodejs运行
	cmd 	node 文件名	

	res.end();
	res.send(): 等同于end + writeHead 设置头信息


## commonjs
	commonjs是模块化的标准，Nodejs是模块化的实现


## 模块化系统
	1.一个js文件就是一个模块，一个模块就是一个对象
	2.文件内容js代码

## Nodejs模块化
### 核心模块
### 文件模块
	module
	exports 暴露 (对象)
	require(文件路径) 调用
	引用是自己建的对象加 ./，引用Nodejs的对象不加


## 包管理工具 npm
	npm init --yes	 		   创建一个描述 初始化 安装package.json
	npm install jquery  		安装一个jQuery包
	npm unstall jquery  		删除一个包
	npm list				   查看安装包  所有包
	npm info jquery  		    查看jquery包
	npm install jquery@版本号    安装某版本号的包
	npm install jquery@latest    更新到最新版本 
	--save--dev		--save 生产环境依赖   --dev开发环境依赖
	-g		全局目录
	npm update -g 	  要更新所有全局软件包
	
	nrm 镜像

## fs  文件系统

```
增删改查
sync  同步
fs.appendFile(file,data[,options],callback) 追加 创建 异步
fs.appendFileSync(file,data[,options],callback) 追加 创建 同步
fs.writeFile(file,data[,options],callback) 从新写入 创建
fs.writeFileSync(file,data[,options],callback) 从新写入创建同步
fs.unlink() 删除文件
fs.rename() 重命名 文件 目录
fs.rmdir  删除目录
文件.isDirectory() 判断文件是否是目录 先 fs.statSync()  调用类
文件.isFile() 判断是否是文件
fs.exists()  判断文件是否存在


```

## 发布一个包

```
npm adduser  添加用户
npm init	初始化包
npm publish  上传
npm unpublish  撤销
```

## path

用于处理文件与目录的路径

```javascript
  path.basename  返回路径的最后文件名
* process.env.PATH  返回win的全局变量
* path.delimiter  提供平台特定的路径分隔符：
	process.env.PATH.split(path.delimiter)  用法
  path.dirname(path)   方法返回一个 path 的目录名
  path.extname(path) 	返回 path 的扩展名 (.html) 
* path.parse(path)  返回一个对象 转换为对象
		{ root: 'D:\\',
  		  dir: 'D:\\wamp\\wamp\\www\\node\\path',
 		  base: 'path.js',
  		  ext: '.js',
  		  name: 'path' }
* path.format(pathObject)  方法会从一个对象返回一个路径字符串
  path.isAbsolute(path) 	方法会判定 path 是否为一个绝对路径。
* path.join([...paths]) ...paths <string> 一个路径片段的序列
	...剩余参数  方法使用平台特定的分隔符把全部给定的 path 片段连		接到一起，并规范化生成的路径  相当于cd 
* path.normalize(path) 方法会规范化给定的 path，并解析 '..' 和 	'.' 片段 格式化 给一个标准路径
path.relative(from, to)  方法返回从 from 到 to 的相对路径（基于当	前工作目录）返回两个路径之间的关系



```

## 全局变量

```
__dirname  		返回当前文件的目录
__filename		返回当前文件的文件名
```

## URL

```javascript
let url = require('url');
let {URL} = url; //结构赋值
let urlobj = new URL('/ni','http://www.baidu.com');//创建

let href = "https://cn.bing.com/search?q=paths&qs=n&form=QBRE&sp=-1&pq=paths&sc=8-5&sk=&cvid=53EE9CE84D4F417BB0A29558FFD011C3";

let obj = url.parse(href,true);// true query转换成对象
console.log(obj);

Class: URL  类
1. url.parse(urlString,boolean,boolean)
parse这个方法可以将一个url的字符串解析并返回一个url的对象
　参数：urlString指传入一个url地址的字符串
　　　第二个参数（可省）传入一个布尔值，默认为false，为true时，返回的url对象中，query的属性为一个对象。
　　　第三个参数（可省）传入一个布尔值，默认为false，为true时，额，我也不知道有什么不同，可以去看看API。
   
2 url.format(urlObj)
　　format这个方法是将传入的url对象编程一个url字符串并返回
  	url.format(urlObj)  将json对象格式化成字符串
　　参数：urlObj指一个url对象   
  
3 url.resolve(from,to)
　　resolve这个方法返回一个格式为"from/to"的字符串  
  返回从根目录指定到当前目录的绝对路径url
	返回结果去除了参数和锚点
	返回结果标准url路径格式
```



## HTTP

```javascript
http.createServer([requestListener])  创建一个服务 返回http.server
requestListener 是一个函数，会被自动添加到 'request' 事件
let server = http.createServer(function (req,res) {
    res.writeHeader(200,{'Content-type':'text/html;charset=utf8'})
    res.write(); 写入信息
    res.end:
});
sever.lister(){
    
}

```

### 搭建一个静态服务器

```javascript
let http = require('http');

let server = http.createServer(function (req,res) {//返回: <http.Server>
    res.writeHeader(200,{'Content-type':'text/html;charset=utf8'});// 设置头信息
    res.write('welcome to my world'); // 写入信息
    res.end();
});
// 方法一
server.listen({
   host:'localhost',
   port:5200,
},function(){
    console.log('you application running:localhost:5200');
});
// 方法二
server.listen(5200,function(){
    console.log('you application running:localhost:5200')
})
```

```javascript
// 引入
let http = require('http');
let url = require('url'); // 处理拿到的地址路径 格式化地址
let fs = require('fs'); 
let path = require('path');
let mime = require('mime');
let data = require('../model/types');


// 创建服务 req 请求信息 res 响应的信息
let server = http.createServer(function (req, res) {//返回: <http.Server>
    // req.url  url.parse(req.url)  找到展示的文件
    let pathname = url.parse(req.url).pathname;
    if (pathname == '/') {
        pathname = '/index.html';
    }
    if (pathname != '/favicon.ico') {
        let p = './static' + pathname;
        let ext = path.extname(pathname).substr(1);
        let type = mime.getType(ext);
        fs.readFile(p, (err, data) => {
            if (err) {
                fs.readFile("./static/404.html", (err404, data404) => {
                    if (err404) {
                        console.log(err404);
                    } else {
                        res.writeHead(200, {'Content-type':type+ ';charset=utf8'});
                        res.write(data404);
                        res.end();
                    }
                })
            } else {
                res.writeHead(200, {'Content-type':type+ ';charset=utf8'});
                res.write(data);
                res.end();
            }
        });
    }
});
// 监听
server.listen({
    host: 'localhost',
    port: 5200,
}, function () {
    console.log('you application running:localhost:5200');
});

/*server.listen(5200, function () {
    console.log('you application running:localhost:5200')
})*/

```

## 事件 events

```javascript
EventEmitter 类
添加事件 on addListener
执行事件 emit（事件类型，参数1，参数2...）
```

## 路由

```javascript
ejs 模板引擎
ejs.renderFile('文件名'，{name:lisi},function(){})
语法 <%  %>
    
    
    路由（Routing）是由一个 URI（或者叫路径）和一个特定的 HTTP 方法（GET、POST 等）组成的，涉及到应用如何响应客户端对某个网站节点的访问。
    
动态路由 ： /new/:nid/  nid 获取 get方式 req.params.nid  对象
		/show?sid=10  查询字符串 get  req.query  对象
        
子路由	    /new/nid/ 
```



## 操作数据库

npm官网下载包MySQL

```javascript
$ npm install mysql //下载MySQL包
var mysql      = require('mysql'); //获取
var connection = mysql.createConnection({//链接数据库
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});
 
```

## express 框架

```javascript
首先假定你已经安装了 Node.js，接下来为你的应用创建一个目录，然后进入此目录并将其作为当前工作目录。

Express 是一个自身功能极简，完全是由路由和中间件构成一个的 web 开发框架：从本质上来说，一个 Express 应用就是在调用各种中间件。

$ mkdir myapp
$ cd myapp
通过 npm init 命令为你的应用创建一个 package.json 文件。 欲了解 package.json 是如何起作用的，请参考 Specifics of npm’s package.json handling。

$ npm init
此命令将要求你输入几个参数，例如此应用的名称和版本。 你可以直接按“回车”键接受默认设置即可，下面这个除外：

entry point: (index.js)
键入 app.js 或者你所希望的名称，这是当前应用的入口文件。如果你希望采用默认的 index.js 文件名，只需按“回车”键即可。

接下来安装 Express 并将其保存到依赖列表中：

$ npm install express --save
如果只是临时安装 Express，不想将它添加到依赖列表中，只需略去 --save 参数即可：

$ npm install express
安装 Node 模块时，如果指定了 --save 参数，那么此模块将被添加到 package.json 文件中 dependencies 依赖列表中。 然后通过 npm install 命令即可自动安装依赖列表中所列出的所有模块。


```

## express 使用模板

```javascript
views, 放模板文件的目录，比如： app.set('views', './views')
view engine, 模板引擎，比如： app.set('view engine', 'jade')
jade 模板引擎

res.render('index',{name:'shenag'},function(){})
```

## express 中间件

```javascript
1、中间件（Middleware） 是一个函数，它可以访问请求对象（request object (req)）, 响应对象（response object (res)）, 和 web 应用中处于请求-响应循环流程中的中间件，一般被命名为 next 的变量。

2、中间件的功能包括：
	执行任何代码。
	修改请求和响应对象。
	终结请求-响应循环。
	调用堆栈中的下一个中间件。
如果当前中间件没有终结请求-响应循环，则必须调用 next() 方法将控制权交给下一个中间件，否则请求就会挂起。

3、Express 应用可使用如下几种中间件：

	应用级中间件
    应用级中间件绑定到 app 对象 使用 app.use() 和 app.METHOD()， 其中， METHOD 是需要处理的 HTTP 请求的方法，例如 GET, PUT, POST 等等，全部小写
	路由级中间件
    
    
	错误处理中间件
	内置中间件
	第三方中间件
    
是一个函数，在匹配到路由之前 或 之后响应文件

```

```javascript

/* 引用express */
let  express = require('express');
let app = express();

/* 引用模板引擎 */
app.set('views', __dirname +'./views');//__dirname 当前目录下
app.set('view engine', 'ejs');

/* 中间件 */
app.use(express.static('static'));

app.get('/',function(req,res){
    res.render('login',function(err,data){
        if(err) throw  err;
        res.end(data);
        //res.send()
    })
});

let server = app.listen(3600,function () {
    console.log('localhost:3600');
});

```

## Express 托管静态文件

```javascript
app.use(express.static('public'));
先会从public文件中找，然后 在执行下面的代码；

通过 Express 内置的 express.static 可以方便地托管静态文件，例如图片、CSS、JavaScript 文件等。
将静态资源文件所在的目录作为参数传递给 express.static 中间件就可以提供静态资源文件的访问了。例如，假设在 public 目录放置了图片、CSS 和 JavaScript 文件，你就可以：

app.use(express.static('public'));


如果你的静态资源存放在多个目录下面，你可以多次调用 express.static 中间件：
app.use(express.static('public'));
app.use(express.static('files'));

访问静态资源文件时，express.static 中间件会根据目录添加的顺序查找所需的文件。

虚拟
如果你希望所有通过 express.static 访问的文件都存放在一个“虚拟（virtual）”目录（即目录根本不存在）下面，可以通过为静态资源目录指定一个挂载路径的方式来实现，如下所示：
app.use('/static', express.static('public'));
现在，你就可以通过带有 “/static” 前缀的地址来访问 public 目录下面的文件了。
```

### 路由级中间件

```javascript
路由级中间件和应用级中间件一样，只是它绑定的对象为 express.Router()。

var router = express.Router();
路由级使用 router.use() 或 router.VERB() 加载。
let express = require('express');
var app = express();
var router = express.Router();

```

## 上传文件

```javascript
var express = require('express')
var multer  = require('multer')
var upload = multer({ dest: 'uploads/' })
 
var app = express()
 
app.post('/profile', upload.single('avatar'), function (req, res, next) {
  // req.file is the `avatar` file 
  // req.body will hold the text fields, if there were any 
})
 
app.post('/photos/upload', upload.array('photos', 12), function (req, res, next) {
  // req.files is array of `photos` files 
  // req.body will contain the text fields, if there were any 
})
 
var cpUpload = upload.fields([{ name: 'avatar', maxCount: 1 }, { name: 'gallery', maxCount: 8 }])
app.post('/cool-profile', cpUpload, function (req, res, next) {
  // req.files is an object (String -> Array) where fieldname is the key, and the value is array of files 
  // 
  // e.g. 
  //  req.files['avatar'][0] -> File 
  //  req.files['gallery'] -> Array 
  // 
  // req.body will contain the text fields, if there were any 
})
```























