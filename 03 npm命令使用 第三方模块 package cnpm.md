# npm

## 包

NodeJS中除了他自己的提供的 核心模块之外，我们还可以自定义模块，或者下载第三方模块。Nodejs中第三放模块由包组成，可以通过包来对一组具有相互依赖关系的模块进行统一管理。

![包](./img/npm.png)

### 完全符合 CommonJs规范的包目录 一般包含如下这些文件。
*  package.json :包描述文件。
*  bin :用于存放可执行二进制文件的目录。
*  lib :用于存放 JavaScript 代码的目录。
*  doc :用于存放文档的目录。

## npm介绍

npm是世界上最大的开放源代码的生态系统。我们可以通过 npm 下载各种各样的包，这些源代码（包）我们可以在 https://www.npmjs.com 找到。
npm  是随同 NodeJS  一起安装的包管理工具，能解决 NodeJS  代码部署上的很多问题，
常见的使用场景有以下几种：

* 允许用户从 NPM 服务器下载别人编写的第三方包到本地使用。(silly-datetime)
* 允许用户从 NPM 服务器下载并安装别人编写的命令行程序(工具)到本地使用。
（supervisor）
*  允许用户将自己编写的包或命令行程序上传到 NPM 服务器供别人使用。

## npm 命令

* 查看版本

```
    npm -v
```

* 安装模块

```
    npm install jquery
```

* 卸载

``` 
    npm uninstall jquery
```

*  查看安装包

```
    npm list 
```

* 查看包信息

```
    npm info jquery
```

* 安装某个版本

```
   npm install jquery@1.8.0
```


## package.json

package.json 定义了这个项目所需要的各种模块,以及项目的配置信息(比如名称、
版本、许可证等元数据)

### 创建package.json

```js
  npm init
  npm init --yes
```

### 安装模块并写入到package.json
```js
   npm install 模块 --save
   npm install 模块 --save-dev
```

> npm install –save–dev：只需开发时依赖的模块devDependencies 
eg: 
babel（转码器，可以将ES6代码转为ES5代码），只需在开发环境是用到webpack
  npm install –save: 生产环境依赖的模块dependencies 
eg: 
jQuery react 

```json
{
  "dependencies" :{
      "ejs":"^2.3.4",
      "express":"^4.13.3",
      "formidable":"~1.0.17"
  }
}
```
> ^表示第一位版本号不变，后面两位取最新的
> ~表示前两位不变，后面一个区最新的
> \* 表示全部最新

## node转换资源

1. 安装nrm

```
npm install nrm -g
```
2. 查看资源


```
nrm ls
```

3. 选择资源 

```
nrm use taobao
```