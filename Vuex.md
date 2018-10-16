# Vuex

## 安装

```
npm install vuex --save

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
```

### Promise

```
Vuex 依赖 Promise

CDN 引入
<script src="https://cdn.jsdelivr.net/npm/es6-promise@4/dist/es6-promise.auto.js"></script>

npm 
npm install es6-promise --save # npm
import 'es6-promise/auto'

自己构建
如果需要使用 dev 分支下的最新版本，您可以直接从 GitHub 上克隆代码并自己构建。

git clone https://github.com/vuejs/vuex.git node_modules/vuex
cd node_modules/vuex
npm install
npm run build

```

## Vuex 是什么

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化 

 



