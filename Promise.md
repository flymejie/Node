# Promise

Promise 对象用于表示一个异步操作的最终状态（完成或失败），以及其返回的值。

```javascript
var promise1 = new Promise(function(resolve, reject) {
  setTimeout(function() { 
    resolve('foo');
  }, 300);
});

promise1.then(function(value) { 
  console.log(value);
  // expected output: "foo"
});

console.log(promise1);
// expected output: [object Promise]

```

## 语法

```js
new Promise( function(resolve, reject) {...} /* executor */  );
```

### 参数

executor

executor是带有 `resolve` 和 `reject` 两个参数的函数 。Promise构造函数执行时立即调用`executor` 函数， `resolve` 和 `reject` 两个函数作为参数传递给`executor`（executor 函数在Promise构造函数返回新建对象前被调用）。`resolve` 和 `reject` 函数被调用时，分别将promise的状态改为*fulfilled（*完成）或rejected（失败）。executor 内部通常会执行一些异步操作，一旦完成，可以调用resolve函数来将promise状态改成*fulfilled*，或者在发生错误时将它的状态改为rejected。

如果在executor函数中抛出一个错误，那么该promise 状态为rejected。executor函数的返回值被忽略。

##　描述

**Promise**对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）。 这让异步方法可以像同步方法那样返回值，但并不是立即返回最终执行结果，而是一个能代表未来出现的结果的promise对象

一个 `Promise`有以下几种状态:

- *pending*: 初始状态，既不是成功，也不是失败状态。
- *fulfilled*: 意味着操作成功完成。
- *rejected*: 意味着操作失败。

pending 状态的 Promise 对象可能触发fulfilled 状态并传递一个值给相应的状态处理方法，也可能触发失败状态（rejected）并传递失败信息。当其中任一种情况出现时，Promise 对象的 `then` 方法绑定的处理方法（handlers ）就会被调用（then方法包含两个参数：onfulfilled 和 onrejected，它们都是 Function 类型。当Promise状态为*fulfilled*时，调用 then 的 onfulfilled 方法，当Promise状态为*rejected*时，调用 then 的 onrejected 方法， 所以在异步操作的完成和绑定处理方法之间不存在竞争）。

因为 `Promise.prototype.then` 和  `Promise.prototype.catch` 方法返回promise 对象， 所以它们可以被链式调用。

![img](https://mdn.mozillademos.org/files/8633/promises.png)

**不要和惰性求值混淆：** 有一些语言中有惰性求值和延时计算的特性，它们也被称为“promises”，例如Scheme. Javascript中的promise代表一种已经发生的状态， 而且可以通过回调方法链在一起。 如果你想要的是表达式的延时计算，考虑无参数的"[箭头方法](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions)":  `f = () =>`*表达式* 创建惰性求值的表达式*，*使用 `f()` 求值。

**注意：** 如果一个promise对象处在fulfilled或rejected状态而不是pending状态，那么它也可以被称为*settled*状态。你可能也会听到一个术语*resolved* ，它表示promise对象处于fulfilled状态。关于promise的术语， Domenic Denicola 的 [States and fates](https://github.com/domenic/promises-unwrapping/blob/master/docs/states-and-fates.md) 有更多详情可供参考。

## 属性[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E5%B1%9E%E6%80%A7)

- `Promise.length`

  length属性，其值总是为 1 (构造器参数的数目).

- [`Promise.prototype`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/prototype)

  表示 `Promise` 构造器的原型.

## 方法[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E6%96%B9%E6%B3%95)

- [`Promise.all(iterable)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

  这个方法返回一个新的promise对象，该promise对象在iterable参数对象里所有的promise对象都成功的时候才会触发成功，一旦有任何一个iterable里面的promise对象失败则立即触发该promise对象的失败。这个新的promise对象在触发成功状态以后，会把一个包含iterable里所有promise返回值的数组作为成功回调的返回值，顺序跟iterable的顺序保持一致；如果这个新的promise对象触发了失败状态，它会把iterable里第一个触发失败的promise对象的错误信息作为它的失败错误信息。Promise.all方法常被用于处理多个promise对象的状态集合。（可以参考jQuery.when方法---译者注）

- [`Promise.race(iterable)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)

  当iterable参数里的任意一个子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象。

- [`Promise.reject(reason)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)

  返回一个状态为失败的Promise对象，并将给定的失败信息传递给对应的处理方法

- [`Promise.resolve(value)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)

  返回一个状态由给定value决定的Promise对象。如果该值是一个Promise对象，则直接返回该对象；如果该值是thenable(即，带有then方法的对象)，返回的Promise对象的最终状态由then方法执行决定；否则的话(该value为空，基本类型或者不带then方法的对象),返回的Promise对象状态为fulfilled，并且将该value传递给对应的then方法。通常而言，如果你不知道一个值是否是Promise对象，使用Promise.resolve(value) 来返回一个Promise对象,这样就能将该value以Promise对象形式使用。

## Promise 原型[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#Promise_%E5%8E%9F%E5%9E%8B)

### 属性[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E5%B1%9E%E6%80%A7_2)

- `Promise.prototype.constructor`

  返回被创建的实例函数.  默认为 [`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 函数.

### 方法[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E6%96%B9%E6%B3%95_2)

- [`Promise.prototype.catch(onRejected)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch)

  添加一个拒绝(rejection) 回调到当前 promise, 返回一个新的promise。当这个回调函数被调用，新 promise 将以它的返回值来resolve，否则如果当前promise 进入fulfilled状态，则以当前promise的完成结果作为新promise的完成结果.

- [`Promise.prototype.then(onFulfilled, onRejected)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)

  添加解决(fulfillment)和拒绝(rejection)回调到当前 promise, 返回一个新的 promise, 将以回调的返回值来resolve.

- [`Promise.prototype.finally(onFinally)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/finally)

  添加一个事件处理回调于当前promise对象，并且在原promise对象解析完毕后，返回一个新的promise对象。回调会在当前promise运行完毕后被调用，无论当前promise的状态是完成(fulfilled)还是失败(rejected)

## 创建Promise[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E5%88%9B%E5%BB%BAPromise)

`Promise` 对象是由关键字 `new` 及其构造函数来创建的。该构造函数会?把一个叫做“处理器函数”（executor function）的函数作为它的参数。这个“处理器函数”接受两个函数——`resolve` 和 `reject` ——作为其参数。当异步任务顺利完成且返回结果值时，会调用 `resolve` 函数；而当异步任务失败且返回失败原因（通常是一个错误对象）时，会调用`reject` 函数。

```
const myFirstPromise = new Promise((resolve, reject) => {
  // ?做一些异步操作，最终会调用下面两者之一:
  //
  //   resolve(someValue); // fulfilled
  // ?或
  //   reject("failure reason"); // rejected
});
```

想要某个函数?拥有promise功能，只需让其返回一个promise即可。

```
function myAsyncFunction(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.onload = () => resolve(xhr.responseText);
    xhr.onerror = () => reject(xhr.statusText);
    xhr.send();
  });
};
```

## 示例[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E7%A4%BA%E4%BE%8B)

### 非常简单的例子[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E9%9D%9E%E5%B8%B8%E7%AE%80%E5%8D%95%E7%9A%84%E4%BE%8B%E5%AD%90)

```
let myFirstPromise = new Promise(function(resolve, reject){
    //当异步代码执行成功时，我们才会调用resolve(...), 当异步代码失败时就会调用reject(...)
    //在本例中，我们使用setTimeout(...)来模拟异步代码，实际编码时可能是XHR请求或是HTML5的一些API方法.
    setTimeout(function(){
        resolve("成功!"); //代码正常执行！
    }, 250);
});

myFirstPromise.then(function(successMessage){
    //successMessage的值是上面调用resolve(...)方法传入的值.
    //successMessage参数不一定非要是字符串类型，这里只是举个例子
    console.log("Yay! " + successMessage);
});
```

### 高级一点的例子[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E9%AB%98%E7%BA%A7%E4%B8%80%E7%82%B9%E7%9A%84%E4%BE%8B%E5%AD%90)

本例展示了 `Promise` 的一些机制。 `testPromise()` 方法在每次点击 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/button) 按钮时被调用，该方法会创建一个promise 对象，使用 [`window.setTimeout()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout) 让Promise等待 1-3 秒不等的时间来填充数据（通过Math.random()方法）。

Promise 的值的填充过程都被日志记录（logged）下来，这些日志信息展示了方法中的同步代码和异步代码是如何通过Promise完成解耦的。

```
'use strict';
var promiseCount = 0;

function testPromise() {
    let thisPromiseCount = ++promiseCount;

    let log = document.getElementById('log');
    log.insertAdjacentHTML('beforeend', thisPromiseCount +
        ') 开始 (<small>同步代码开始</small>)<br/>');

    // 新构建一个 Promise 实例：使用Promise实现每过一段时间给计数器加一的过程，每段时间间隔为1~3秒不等
    let p1 = new Promise(
        // resolver 函数在 Promise 成功或失败时都可能被调用
       (resolve, reject) => {
            log.insertAdjacentHTML('beforeend', thisPromiseCount +
                ') Promise 开始 (<small>异步代码开始</small>)<br/>');
            // 创建一个异步调用
            window.setTimeout(
                function() {
                    // 填充 Promise
                    resolve(thisPromiseCount);
                }, Math.random() * 2000 + 1000);
        }
    );

    // Promise 不论成功或失败都会调用 then
    // catch() 只有当 promise 失败时才会调用
    p1.then(
        // 记录填充值
        function(val) {
            log.insertAdjacentHTML('beforeend', val +
                ') Promise 已填充完毕 (<small>异步代码结束</small>)<br/>');
        })
    .catch(
        // 记录失败原因
       (reason) => {
            console.log('处理失败的 promise ('+reason+')');
        });

    log.insertAdjacentHTML('beforeend', thisPromiseCount +
        ') Promise made (<small>同步代码结束</small>)<br/>');
}
```

点击下面的按钮可以看到示例代码运行的效果，前提是你的浏览器支持 `Promise`。快速点击按钮多次你会观察到Promises填充值的过程。

在 CodePen 中打开在 JSFiddle 中打开

## 使用 XHR 加载图像[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E4%BD%BF%E7%94%A8_XHR_%E5%8A%A0%E8%BD%BD%E5%9B%BE%E5%83%8F)

另一个用了 Promise 和[ XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) 加载一个图像的例子可在MDN GitHub[promise-test](https://github.com/mdn/js-examples/tree/master/promises-test) 中找到。 你也可以[看这个实例](https://mdn.github.io/js-examples/promises-test/)。每一步都有注释可以让你详细的了解Promise和XHR架构。

## 规范[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E8%A7%84%E8%8C%83)

| 规范                                                         | 状态     | 备注                 |
| ------------------------------------------------------------ | -------- | -------------------- |
| [ECMAScript 2015 (6th Edition, ECMA-262) Promise](https://www.ecma-international.org/ecma-262/6.0/#sec-promise-objects) | Standard | ECMA标准中的首次定义 |
| [ECMAScript Latest Draft (ECMA-262) Promise](https://tc39.github.io/ecma262/#sec-promise-objects) | Draft    |                      |

## 浏览器兼容性[Section](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise#%E6%B5%8F%E8%A7%88%E5%99%A8%E5%85%BC%E5%AE%B9%E6%80%A7)

Update compatibility data on GitHub

| Desktop                                                      | Mobile         | Server          |                         |              |                |                        |                    |                |                     |                         |                 |                        |                 |                           |
| ------------------------------------------------------------ | -------------- | --------------- | ----------------------- | ------------ | -------------- | ---------------------- | ------------------ | -------------- | ------------------- | ----------------------- | --------------- | ---------------------- | --------------- | ------------------------- |
| Chrome                                                       | Edge           | Firefox         | Internet Explorer       | Opera        | Safari         | Android webview        | Chrome for Android | Edge Mobile    | Firefox for Android | Opera for Android       | iOS Safari      | Samsung Internet       | Node.js         |                           |
| Basic support                                                | Full support32 | Full supportYes | Full support29          | No supportNo | Full support19 | Full support8          | Full support4.4.3  | Full support32 | Full supportYes     | Full support29          | Full supportYes | Full support8          | Full supportYes | Full support0.12          |
| `Promise()` constructor                                      | Full support32 | Full supportYes | Full support29Notes打开 | No supportNo | Full support19 | Full support8Notes打开 | Full support4.4.3  | Full support32 | Full supportYes     | Full support29Notes打开 | Full supportYes | Full support8Notes打开 | Full supportYes | Full support0.12Notes打开 |
| [`all`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/all) | Full support32 | Full supportYes | Full support29          | No supportNo | Full support19 | Full support8          | Full support4.4.3  | Full support32 | Full supportYes     | Full support29          | Full supportYes | Full support8          | Full supportYes | Full support0.12          |
| [`prototype`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/prototype) | Full support32 | Full supportYes | Full support29          | No supportNo | Full support19 | Full support8          | Full support4.4.3  | Full support32 | Full supportYes     | Full support29          | Full supportYes | Full support8          | Full supportYes | Full support0.12          |
| [`catch`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch) | Full support32 | Full supportYes | Full support29          | No supportNo | Full support19 | Full support8          | Full support4.4.3  | Full support32 | Full supportYes     | Full support29          | Full supportYes | Full support8          | Full supportYes | Full support0.12          |
| [`finally`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/finally) | Full support63 | No supportNo    | Full support58          | No supportNo | Full support50 | Full support11.1       | Full support63     | Full support63 | No supportNo        | Full support58          | Full support50  | Full support11.1       | No supportNo    | Full support10.0.0        |
| [`then`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/then) | Full support32 | Full supportYes | Full support29          | No supportNo | Full support19 | Full support8          | Full support4.4.3  | Full support32 | Full supportYes     | Full support29          | Full supportYes | Full support8          | Full supportYes | Full support0.12          |
| [`race`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/race) | Full support32 | Full supportYes | Full support29          | No supportNo | Full support19 | Full support8          | Full support4.4.3  | Full support32 | Full supportYes     | Full support29          | Full supportYes | Full support8          | Full supportYes | Full support0.12          |
| [`reject`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject) | Full support32 | Full supportYes | Full support29          | No supportNo | Full support19 | Full support8          | Full support4.4.3  | Full support32 | Full supportYes     | Full support29          | Full supportYes | Full support8          | Full supportYes | Full support0.12          |
| [`resolve`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve) | Full support32 | Full supportYes | Full support29          | No supportNo | Full support19 | Full support8          | Full support4.4.3  | Full support32 | Full supportYes     | Full support29          | Full supportYes | Full support8          | Full supportYes | Full support0.12          |

### Legend

- Full support 

  Full support

- No support 

  No support

- See implementation notes.

  See implementation notes.



