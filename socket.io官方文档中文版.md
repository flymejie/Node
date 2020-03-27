# socket.io官方文档中文版



原文链接：[www.shuaihua.cc](https://link.juejin.im/?target=http%3A%2F%2Fwww.shuaihua.cc%2Farticle%2Fsocket-io-official-document-translate-part-one%2F)

[![img](data:image/svg+xml;utf8,)](https://juejin.im/entry/59b126c46fb9a02487556964/detail)

最近对实时通信感兴趣，就研究socket.io的官方文档，读完之后觉得也就几个常用的方法来回的调，关键是能在实际应用场景中玩出花样来。帅华君在阅读文档的过程中顺便把官方文档翻译成中文，方便初学者入门，不过建议还是要去socket.io官网看看。

[官方文档英文版](https://link.juejin.im/?target=https%3A%2F%2Fsocket.io%2Fdocs%2F)

------

# **一、概述**

## 1、如何使用

**安装**

```
$ npm install socket.io
```

##### **使用Node http服务器搭建**

**服务器端(app.js)**

```
var app = require('http').createServer(handler)
var io = require('socket.io')(app);
var fs = require('fs');

app.listen(80);

function handler (req, res) {
  fs.readFile(__dirname + '/index.html',
  function (err, data) {
    if (err) {
      res.writeHead(500);
      return res.end('Error loading index.html');
    }

    res.writeHead(200);
    res.end(data);
  });
}

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});
```

**客户端(index.html)**

```
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>
```

##### **使用Express3/4**

**服务器端（app.js）**

```
var app = require('express')();
var server = require('http').Server(app);
var io = require('socket.io')(server);

server.listen(80);

app.get('/', function (req, res) {
  res.sendfile(__dirname + '/index.html');
});

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});
```

**客户端（index.html）**

```
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io.connect('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>
```

##### **使用Express 2.X**

**服务器端（app.js）**

```
var app = require('express').createServer();
var io = require('socket.io')(app);

app.listen(80);

app.get('/', function (req, res) {
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function (socket) {
  socket.emit('news', { hello: 'world' });
  socket.on('my other event', function (data) {
    console.log(data);
  });
});
```

**客户端（index.html）**

```
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io.connect('http://localhost');
  socket.on('news', function (data) {
    console.log(data);
    socket.emit('my other event', { my: 'data' });
  });
</script>
```

##### **发送和接收事件推送**

Socket.io允许你**触发**或**响应**自定义的事件，除了**connect**，**message**，**disconnect**这些事件的名字不能使用之外，你可以触发任何自定义的事件名称。

**服务器端**

```
// 注意，io(<端口号>) 将为你创建一个http服务。
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  io.emit('this', { will: 'be received by everyone'});

  socket.on('private message', function (from, msg) {
    console.log('I received a private message by ', from, ' saying ', msg);
  });

  socket.on('disconnect', function () {
    io.emit('user disconnected');
  });
});
```

##### **创建你自己的路由**

如果你只需要掌控一个应用的全部的消息和触发的事件，那么使用默认的**/**命名空间即可。如果你想要利用第三方代码，或者分享你的代码给别人，socket.io提供了一种命名一个socket的途径。

使用多路由控制一条单一的连接是有好处的。比如下方的示例代码，客户端发起两个**WebSocket**连接，而服务器端使用多路由技术仅仅只需要建立一个连接。

**服务器端（app.js）**

```
var io = require('socket.io')(80);
var chat = io
  .of('/chat')
  .on('connection', function (socket) {
    socket.emit('a message', {
        that: 'only'
      , '/chat': 'will get'
    });
    chat.emit('a message', {
        everyone: 'in'
      , '/chat': 'will get'
    });
  });

var news = io
  .of('/news')
  .on('connection', function (socket) {
    socket.emit('item', { news: 'item' });
  });
```

**客户端（index.html）**

```
<script>
  var chat = io.connect('http://localhost/chat')
    , news = io.connect('http://localhost/news');

  chat.on('connect', function () {
    chat.emit('hi!');
  });

  news.on('news', function () {
    news.emit('woot');
  });
</script>
```

##### 发送不确定能否准确送达到客户端的消息

有些时候，一些发送的消息会在传输过程中不慎丢失（由于网络故障或者其他问题导致，或者由于他们是通过长连接轮询的方式存在与请求-响应循环列表中）。

这种情况下，你可能想要发送这样的一类消息，叫做**易挥发消息**（volatile message）。

**服务器端**

```
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  var tweets = setInterval(function () {
    getBieberTweet(function (tweet) {
      socket.volatile.emit('bieber tweet', tweet);
    });
  }, 100);

  socket.on('disconnect', function () {
    clearInterval(tweets);
  });
});
```

##### 正在发送和正在接受的数据（消息确认机制 acknowledgements）

有些时候，客户端会需要**确认**向服务器端发送的事件是否在服务器端正确执行了。

为了能够实现这一功能，只需简单的通过一个回调函数，放置与**.send()**或者**.emit()**方法的最后一个参数即可，值得一提的是，当你使用**.emit()**，这个确认是有你来完成的，也就是说你可以在这里一直的发送数据。

**服务器端（app.js）**

```
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  socket.on('ferret', function (name, fn) {
    fn('woot');
  });
});
```

**客户端（index.html）**

```
<script>
  var socket = io(); // TIP: io() with no args does auto-discovery
  socket.on('connect', function () { // TIP: you can avoid listening on `connect` and listen on events directly too!
    socket.emit('ferret', 'tobi', function (data) {
      console.log(data); // data will be 'woot'
    });
  });
</script>
```

##### 广播消息给除当前客户端之外的所有在线客户端

为了实现广播消息这一功能，简单的添加一个**broadcast**标志给**emit**和**send**方法的calls，广播意味着发送一个给所有socket（客户端）的消息，不过除了触发这一广播消息的socket（客户端）之外。

**服务器端（app.js）**

```
var io = require('socket.io')(80);

io.on('connection', function (socket) {
  socket.broadcast.emit('user connected');
});
```

**客户端（index.html）**

```
<script>
  var socket = io('http://localhost/');
  socket.on('connect', function () {
    socket.send('hi');

    socket.on('message', function (msg) {
      // my msg
    });
  });
</script>
```

如果你想要深入学习可以打开这个页面，学习[Engine.IO](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fsocketio%2Fengine.io)，这（**Engine.IO**）一框架是Socket.IO的基础。

## 二、服务器端API

##### Server

通过 **require(‘socket.io’)** 暴露。

------

##### new Server(httpServer[, options]);

```
const Server = require('socket.io');
new Server(httpServer[, options])
```

**参数说明：**

- httpServer (http.Server) 需要绑定的服务。
- options (对象)
  - path (字符串)：捕获webSocket连接的路径名，默认为（**/socket.io**）。
  - serverClient (布尔型)：是否为本地文件提供服务，默认为（**true**）。
  - adapter (Adapter对象)：使用哪一个适配器对象，默认的指向**Adapter**类的一个实例，详情跳转至[socket.io-adapter](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fsocketio%2Fsocket.io-adapter)
  - origins (字符串)：规定被允许的域，默认为（*） 。
  - parser （Parser对象）：指向一个parser对象，默认使用与socket.io相关联的[socket.io-parser](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fsocketio%2Fsocket.io-parser)

使用**new**关键字和不使用**new**关键字均可实例化一个socket连接。

```
const io = require('socket.io')();
// or
const Server = require('socket.io');
const io = new Server();
```

对于**engine.io**，使用相同的配置项即可，详情查看[engine.io的配置项参考](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fsocketio%2Fengine.io%23methods-1)。

其他的配置项：

- pingTimeout (数值型)：客户端在没有收到服务器端的响应时，等待多少毫秒数，，默认是60000毫秒（即1分钟）。
- pingInterval (数值型)：服务器端在发送响应包前延迟多少毫秒，默认为25000毫秒（即25秒）。

这两个参数将会影响的是响应延迟，客户端在知道服务不可用之前仍然需要等待一段时间。举个例子，如果下行TCP连接没有关闭，大概是由于网络故障，但是客户端不得不等待**pingTimeout**+**pingInterval**这个长的毫秒数才能得知**disconnect**（未连接成功）这一事件。

- transports （Array 包含一系列字符串元素的数组）：这一选项规定了允许哪些连接方式，默认的（**[‘polling’,‘websocket’]**）。

**注意**：这一点很重要，默认的，会使用长轮询的连接方式作为第一手方案，随后如果设备支持的话会升级到使用WebSocket，如果**transports**选项的值设置为**[‘websocket’]**，则意味着直接使用WebSocket方式建立连接，并且如果这一连接方式不能使用，也不会自动切换到备用的链接方案（**polling**），因此目前建议使用默认的设置即可，除非你明白确信使用场景和你想要做什么。

```
const server = require('http').createServer();

const io = require('socket.io')(server, {
  path: '/test',
  serveClient: false,
  // below are engine.IO options
  pingInterval: 10000,
  pingTimeout: 5000,
  cookie: false
});

server.listen(3000);
```

------

##### new Server(port[, options]);

- port （数值型）：要监听的端口号（如此一来 **httpServer**将会被自动创建）。
- options （对象）：同上方的配置

```
const server = require('http').createServer();

const io = require('socket.io')(3000, {
  path: '/test',
  serveClient: false,
  // below are engine.IO options
  pingInterval: 10000,
  pingTimeout: 5000,
  cookie: false
});
```

------

##### new Server(options);

- options （对象）：同上方配置项

```
const io = require('socket.io')({
  path: '/test',
  serveClient: false,
});

// either
const server = require('http').createServer();

io.attach(server, {
  pingInterval: 10000,
  pingTimeout: 5000,
  cookie: false
});

server.listen(3000);

// or
io.attach(3000, {
  pingInterval: 10000,
  pingTimeout: 5000,
  cookie: false
});
```

------

##### server.sockets

- （命名空间） 默认的命名空间为**/**。

------

##### server.serverClient([value]);

- value （布尔型）
- Return Server | Boolean

如果**value**的值为**true**，则绑定的服务将会对本地文件提供服务。默认的为**true**。这个方法在**attach**函数被调用之后再调用它不会产生任何效果。如果没有提供任何参数，这个方法将会返回当前的值。

```
// 通过http server的情况可以直接这样写。
const io = require('socket.io')(http, { serveClient: false });

// 或者不通过server的情况，你可以这样调用serverClient方法，记得需要在attach之前调用。
const io = require('socket.io')();
io.serveClient(false);
io.attach(http);
```

------

##### server.path([value]);

- value （字符串）
- Return Server | String

设置路径值，指定哪一个**engine.io**和静态文件将被提供服务。默认的路径为**/socket.io**。如果没有提供参数这个方法将会返回当前的路径值。

```
const io = require('socket.io')();
io.path('/myownpath');

// 客户端
const socket = io({
  path: '/myownpath'
});
```

------

##### server.adapter([value]);

- value （Adapter）
- Return Server | Adapter

设置适配器的值，默认的指向一个Adapter的实例。如果没有提供参数则返回当前的值。

```
const io = require('socket.io')(3000);
const redis = require('socket.io-redis');
io.adapter(redis({ host: 'localhost', port: 6379 }));
```

------

##### server.origins([value]);

- value （字符串）
- Return Server | String

设置被允许的域的值，默认的任何域都被允许。如果没有提供参数这个方法将会返回当前的值。

```
io.origins(['foo.example.com:443']);
```

------

##### server.origins(fn);

- fn (Function)
- Return Server

提供一个函数，这个函数将携带两个参数，分别是客户端请求的**origin:String**和一个回调函数**callback(err, succcess)**，开发者可以判断origin这个参数是否为希望接收请求的域，**success**是一个布尔值，代表着提供的这个域是否被允许，如果允许该域则填入**true**，如果不允许则填入**false**即可，err参数如无可填入**null**。

**潜在的缺点**

- 在一些情况下，当无法准确的判断域时，将会自动的使用（*），即全部允许。
- 这个函数将会对所有的请求都执行一次，这个函数将尽可能快的执行完毕。
- 如果**socket.io**和Express一起使用，CORS头信息将会仅对socket.io的请求有效，因此Express可以使用[Cors](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fexpressjs%2Fcors)

```
io.origins((origin, callback) => {
  if (origin !== 'https://foo.example.com') {
    return callback('origin not allowed', false);
  }
  callback(null, true);
});
```

------

##### server.attach(httpServer[, options]);

- httpServer （httpServer）要依附的http服务
- option （对象）

依附于这个Server到一个httpServer上的engine.io实例，并携带options配置项（可有可无）。

------

##### server.listen(httpServer[, options]);

和**server.attach(port[, options])**功能相同。

------

##### server.bind(engine);

- engine （engine.Server）
- Return Server

推荐这样使用，绑定这一服务到指定的Engine.io实例上。

------

##### server.onconnections(socket);

- socket （engine.Socket）
- Return Server

推荐使用，创建一个新的**socket.io**客户端。

------

##### server.of(nsp)

- nsp （字符串）
- Return 命名空间

通过路径名称来标志**nsp**（命名空间），初始化并且返回给定的命名空间。如果命名空间已经被初始化了，将立即返回。

```
const adminNamespace = io.of('/admin');
```

------

##### server.close([callback]);

- callback (Function)

关闭这个socket.io服务。这个回调函数是可选的（可填可不填），这个回调函数将在所有连接被关闭后执行。

```
const Server = require('socket.io');
const PORT   = 3030;
const server = require('http').Server();

const io = Server(PORT);

io.close(); // Close current server

server.listen(PORT); // PORT is free to use

io = Server(server);
```

------

#### Namespace

代表一些列的sockets的链接所指向的作用域的标志，这些标志通过路径名来唯一确定（比如**/chat**这一路径名，或者叫做命名空间）。

一个客户端总是先尝试着连接到**/**（主要的命名空间），然后潜在的连接到其他可用的命名空间（当使用相同的下行连接和多路由机制时）。

------

##### [namespace.name](https://link.juejin.im/?target=http%3A%2F%2Fnamespace.name)

- （String）

命名空间标识符属性。

------

##### namespace.connected

- （Object ）

连接到这一命名空间的**socket**对象的哈希码们，索引为**id**。

------

##### namespace.adapter

- （Adapter）

**Adapter**被用于命名空间，当使用给予redis的**Adapter**时是很有用的。它将会通过你的集群暴露一些方法来管理sockets和房间。

**注意**：注命名空间的适配器可以这样使用，**io.of(’/’).adapter。

------

##### [namespace.to](https://link.juejin.im/?target=http%3A%2F%2Fnamespace.to)(room);

- room （String）
- Return Namespace for chaining

设置修改器，用来将随后的事件发射到到指定的房间号，这样只有存在于指定房间的socket客户端才可接受到广播消息。

为了触发多个房间，你可以多次调用**to**方法。

```
const io = require('socket.io')();
const adminNamespace = io.of('/admin');

adminNamespace.to('level1').emit('an event', { some: 'data' });
```

------

##### [namespace.in](https://link.juejin.im/?target=http%3A%2F%2Fnamespace.in)(room)

用法同**namespace.to(room)**

------

##### namespace.emit(eventName[, …args])

- eventName （String）
- args

触发一个事件给所有的连接中的客户端。下方代码的两种示例作用是等价的。

```
const io = require('socket.io')();
io.emit('an event sent to all connected clients'); // main namespace

const chat = io.of('/chat');
chat.emit('an event sent to all connected clients in chat namespace');
```

**注意**：从命名空间触发的事件不支持消息送达确认。

------

##### namespace.client(callback)

- callback （Function）

获取一系列连接到当前命名空间（路由）的客户端ID（会穿越所有节点）。

```
const io = require('socket.io')();
io.of('/chat').clients((error, clients) => {
  if (error) throw error;
  console.log(clients); // => [PZDoMHjiu8PYfRiKAAAF, Anw2LatarvGVVXEIAAAD]
});
```

示例，获得所有在指定命名空间的房间里的客户端们。

```
io.of('/chat').in('general').clients((error, clients) => {
  if (error) throw error;
  console.log(clients); // => [Anw2LatarvGVVXEIAAAD]
});
```

和广播一样，默认的，将获取所有从默认的**/**命名空间过来的客户端们。

```
io.clients((error, clients) => {
  if (error) throw error;
  console.log(clients); // => [6em3d4TJP8Et9EMNAAAA, G5p55dHhGgUnLUctAAAB]
});
```

------

##### namespace.use(fn)

- fn (Function)

注册一个中间件，这个函数将对所有流经的socket执行操作，并且还会已接受传参的方式获得流经的socket，并且流经到当前中间件之后，可以可选择的确定是否流经到下一个中间件。

当错误信息经过中间件，回调函数将会发送一个特殊的错误信息给客户端。

```
io.use((socket, next) => {
  if (socket.request.headers.cookie) return next();
  next(new Error('Authentication error'));
});
```

------

##### Event: ‘connect’

- socket （socket） 客户端的socket连接实例

当有一个来自客户端的连接时触发该事件。

```
io.on('connect', (socket) => {
  // ...
});

io.of('/admin').on('connect', (socket) => {
  // ...
});
```

------

##### Event: ‘connection’

用法同**Event: ‘connect’**。

------

##### Flag: ‘Volatile’

设置修改器，将随后的事件触发导向这样一种情况：即如果当客户端没有做好接受信息的准备时（可能由于网络故障或者其他问题导致的，或者连接方式采用长轮询的方式，而恰好响应接受消息的事件此时还在请求-响应循环列表中未被触发），那么允许服务器发送的数据丢失。

```
io.volatile.emit('an event', { some: 'data' }); // the clients may or may not receive it
```

------

##### Flag: ‘local’

设置修改器，将随后的事件导向这样一种情况：即事件数据仅广播给当前节点（当使用了[Redis adapter](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fsocketio%2Fsocket.io-redis)）。

```
io.local.emit('an event', { some: 'data' });
```

------

##### Socket

socket是与客户端浏览器交互的基石。socket属于一个确定的命名空间（默认为**/**），并且使用下行客户端沟通讯息。

值得注意的是，这里所指的socket和下行TCP/IP的socket不是一回事儿，这里所指的socket只是一个类名而已。

在每一个命名空间内，你可以定义任意的频道（被叫做房间room的东西），如此socket就可以加入房间或者离开房间。房间的机制使得服务器端可以同时给一组socket广播消息。

socket类集成了**EventEmitter**，socket类重写了**emit**方法，并且不会修改其他的**EventEmitter**方法、这里所有的以**EventMitter**的形式出现的方法们均是通过**EventEmitter**实现。

##### [socket.id](https://link.juejin.im/?target=http%3A%2F%2Fsocket.id)

- （返回字符串）

一个独一无二的针对当前会话socket的标志，来自下行客户端。

------

##### socket.rooms

- （返回对象）

遗传哈希字符串，用来标志当前客户端所在的房间号，通过房间名称建立索引。

```
io.on('connection', (socket) => {
  socket.join('room 237', () => {
    let rooms = Objects.keys(socket.rooms);
    console.log(rooms); // [ <socket.id>, 'room 237' ]
  });
});
```

------

##### socket.client

- （Client）

下行客户端对象的引用。

------

##### socket.conn

- （engine.Socket）

下行客户端传输连接的引用（[engine.io](https://link.juejin.im/?target=http%3A%2F%2Fengine.io) socket 对象），这个允许进入到IO的传输层，不过仍然是实际的TCP/IP socket的一种抽象表示。

------

##### socket.handshake

- （对象）

握手（handshake）细节：

```
{
  headers: /* the headers sent as part of the handshake */,
  time: /* the date of creation (as string) */,
  address: /* the ip of the client */,
  xdomain: /* whether the connection is cross-domain */,
  secure: /* whether the connection is secure */,
  issued: /* the date of creation (as unix timestamp) */,
  url: /* the request URL string */,
  query: /* the query object */
}
```

用例

```
io.use((socket, next) => {
  let handshake = socket.handshake;
  // ...
});

io.on('connection', (socket) => {
  let handshake = socket.handshake;
  // ...
});
```

------

##### socket.use(fn)

- fn （Function）

注册中间件，当任何讯息流经该中间件时执行中间件中的内容，该中间件会接受参数，也可以判断是否阻断后续中间件的执行。

当发生错误，错误将会通过中间件的回调函数，直接发送一个特殊的错误数据包到客户端。

```
io.on('connection', (socket) => {
  socket.use((packet, next) => {
    if (packet.doge === true) return next();
    next(new Error('Not a doge error'));
  });
});
```

------

##### socket.send([…args][, ack])

- args
- ack （Function）
- Return Socket

发送一个**message**事件，

------

##### socket.emit(eventName[, …args][, ack])

（重写 EventEmitter.emit方法）

- eventName （字符串）
- args
- ack （Function）
- Return Socket

通过事件名来触发事件给指定的socket，任意多的参数都可被传入，支持所有可序列化的数据结构。包括**Buffer**。

```
socket.emit('hello', 'world');
socket.emit('with-binary', 1, '2', { 3: '4', 5: new Buffer(6) });
```

其中**ack**参数是可选的（用意确认客户端是否接受到讯息，或者对信息做处理并返回给服务器端），并且将被客户应答。

```
io.on('connection', (socket) => {
  socket.emit('an event', { some: 'data' });

  socket.emit('ferret', 'tobi', (data) => {
    console.log(data); // data will be 'woot'
  });

  // the client code
  // client.on('ferret', (name, fn) => {
  //   fn('woot');
  // });

});
```

------

##### socket.on(eventName, callback)

（继承子**EventEmitter**）

- eventName （字符串）
- callback （Function）
- Return Socket

为给定的事件注册一个新的事件处理器。

```
socket.on('news', (data) => {
  console.log(data);
});
// with several arguments
socket.on('news', (arg1, arg2, arg3) => {
  // ...
});
// or with acknowledgement
socket.on('news', (data, callback) => {
  callback(0);
});
```

------

##### socket.once(eventName, listener)

------

##### socket.removeListener(eventName, listener)

------

##### socket.removeAllListener([eventName])

------

##### socket.eventNames()

继承自**EventEmitter**（还有其他在这里未提及的方法），查看Node.js的官方文档对**events**模块的说明。

------

##### socket.join(room[, callback])

- room （字符串）
- callback （Function）
- Return Socket for chaining

添加客户端到**room**房间内，并且执行可选择的回调函数。

```
io.on('connection', (socket) => {
  socket.join('room 237', () => {
    let rooms = Objects.keys(socket.rooms);
    console.log(rooms); // [ <socket.id>, 'room 237' ]
    io.to('room 237', 'a new user has joined the room'); // broadcast to everyone in the room
  });
});
```

加入房间的过程被**Adapter**适配器处理。

为了更方便开发者，每一个socket自动的通过他自己的id标志创建了一个只属于他自己的房间，这样做，使得当前socket和其他socket之间的广播变得更容易。

```
io.on('connection', (socket) => {
  socket.on('say to someone', (id, msg) => {
    // send a private message to the socket with the given id
    socket.to(id).emit('my message', msg);
  });
});
```

------

##### socket.leave(room[, callback])

- room （字符串）
- callback （Function）
- Return Socket for chaining

从指定的房间里移除客户端，并且可选择的执行一个异常回调函数。

**与当客户端的连接丢失后，会自动的将其从房间移除**

------

##### [socket.to](https://link.juejin.im/?target=http%3A%2F%2Fsocket.to)(room)

- room （字符串）
- Return Socket for chaining

设置修改器，使得随后的事件导向这样的一种情况：即仅向当前房间的客户端广播消息（主动广播消息的一方除外）。

为了能对多个房间触发同一个广播，你需要给多个房间链式的执行几次**to**方法。

```
io.on('connection', (socket) => {
  // to one room
  socket.to('others').emit('an event', { some: 'data' });
  // to multiple rooms
  socket.to('room1').to('room2').emit('hello');
  // a private message to another socket
  socket.to(/* another socket id */).emit('hey');
});
```

**注意**：广播消息下执行**emit**方法，是无法传入确认消息是否接收的回调函数的，原因你懂的。

------

##### [socket.in](https://link.juejin.im/?target=http%3A%2F%2Fsocket.in)(room)

用法同 [socket.to](https://link.juejin.im/?target=http%3A%2F%2Fsocket.to)(room)

------

##### socket.compress(value)

- value （布尔型）是否对数据包进行压缩
- Return Socket for chaining

设置修改器，将随后的事件导向这样一种情况，仅对设置为**true**的数据进行压缩，如果不调用该方法，默认为**true**。

```
io.on('connection', (socket) => {
  socket.compress(false).emit('uncompressed', "that's rough");
});
```

------

##### socket.disconnect(close)

- close （布尔型）是否关闭下行连接
- Return Socket

关闭对客户端的链接，如果close的值为**true**，则关闭下行连接，否则，仅仅关闭命名空间。

```
io.on('connection', (socket) => {
  socket.compress(false).emit('uncompressed', "that's rough");
});
```

------

##### Flag: ‘broadcast’

设置修改器，是的随后的事件导向这样一种情况，即除了主动广播消息的客户端以外，将随后的事件消息广播给所有的socket。

```
io.on('connection', (socket) => {
  socket.broadcast.emit('an event', { some: 'data' }); // everyone gets it but the sender
});
```

------

##### Flag: ‘volatile’

设置修改器，使得随后的事件导向这样一种情况，允许客户端在没有做好接受数据的准备时丢失消息数据，详细翻译去上边找哈~。

```
io.on('connection', (socket) => {
  socket.volatile.emit('an event', { some: 'data' }); // the client may or may not receive it
});
```

------

##### Event: ‘disconnect’

- reason （字符串）丢失连接的原因（客户端与服务器端相同）

丢失连接时。

```
io.on('connection', (socket) => {
  socket.on('disconnect', (reason) => {
    // ...
  });
});
```

------

##### Event: ‘disconnecting’

- reason （字符串） 丢失连接的原因（客户端与服务器端相同）

当客户端丢失连接后执行（此时还为离开房间**rooms**）。

```
io.on('connection', (socket) => {
  socket.on('disconnecting', (reason) => {
    let rooms = Object.keys(socket.rooms);
    // ...
  });
});
```

这里有一些保留事件（**connect**，**newListener**和**removeListener**），这些名臣不能用与事件自定义名称。

------

##### Client

**client**类代表从客户端过来的传输连接。一个客户端和属于不同命名空间的多路复用的socket有关联，即client客户端仅一个，而client可以通过访问不同的命名空间创建多个socket连接。

------

##### client.conn

- (engine.Socket)

下行engine.io连接的引用。

------

##### client.request

- （请求）

可以看作为一个代理，返回请求的引用。了解请求头信息，如Cookie或者User-Agent的知识是有帮助的。