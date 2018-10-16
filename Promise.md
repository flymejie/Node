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





