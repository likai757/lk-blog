---
title: JavaScript 深入浅出（1）
date: 2016-08-15 19:10:00
categories:
- js
tags:
- javascript
---

> **If you can’t explain it simply,you don’t understand it well enough**

> 这句话源自爱因斯坦语录，在一个互联网知识资源无限大的环境里，我们需要学习的不仅仅是学习知识本身，更需要的是一种学习的能力。

## JS简述

JS是一门宿主脚本语言，早期是依附于Web浏览器，随后Ryan Dahl推出了基于V8引擎开发Nodejs，使得JS有了读写文件，创建网络服务的能力，自此JS就不再受限于浏览器，也开始被广泛的应用于服务器端，提供网络服务。

## Nodejs发展史
[Nodejs官方网站](https://nodejs.org/zh-cn/)

> 2009年2月，Ryan Dahl在博客上宣布准备基于V8创建一个轻量级的Web服务器并提供一套库。
>
> 2009年5月，Ryan Dahl在GitHub上发布了最初版本的部分Node.js包，随后几个月里，有人开始使用Node.js开发应用。
>
> 2009年11月和2010年4月，两届JSConf大会都安排了Node.js的讲座。
>
> 2010年年底，Node.js获得云计算服务商Joyent资助，创始人Ryan Dahl加入Joyent全职负责Node.js的发展。
>
> 2011年7月，Node.js在微软的支持下发布Windows版本。


## ECMAScript标准

ECMAScript是JS语言及语法的标准，在我们现在的项目中，主要以ECMAScript 2015年发布的 ES6 为主。

[ES6新特性-引用阮一峰(中文版)](http://es6.ruanyifeng.com/)

> 1	1997年6月	首版
>
> 2	1998年6月	格式修正，以使得其形式与ISO/IEC16262国际标准一致
>
> 3	1999年12月	强大的正则表达式，更好的词法作用域链处理，新的控制指令，异常处理，错误定义更加明确，数据输出的格式化及其它改变
>
> 4	放弃	由于关于语言的复杂性出现分歧,第4版本被放弃,其中的部分成为了第5版本及Harmony的基础。
>
> 5	2009年12月[4]	新增“严格模式（strict mode）”，一个子集用作提供更彻底的错误检查,以避免结构出错。澄清了许多第3版本的模糊规范,and accommodates behaviour of real-world implementations that differed consistently from that specification。增加了部分新功能,如getters及setters,支持JSON以及在物件属性上更完整的反射。
>
> 6	2015年6月	多个新的概念和语言特性。ECMAScript Harmony将会以“ECMAScript 6”发布。
>
> 7	2016年6月	多个新的概念和语言特性

## npm 包管理器

NPM是nodejs的包管理器， 随着Nodejs的版本的推出，随之而来的问题是第三方代码库的引入和管理问题，同iOS中Cocoapods，与Android中Gradle解决的问题相同，后面会专门为npm单独，这里不再详细赘述。

[npm官方安装文档](https://docs.npmjs.com/getting-started/installing-node)

这里推荐两个命令行的Node版本管理工具(n & nvm)
[Node版本管理工具](http://weizhifeng.net/node-version-management-via-n-and-nvm.html)

#### n
> [`n`](https://github.com/tj/n) 是 [TJ Holowaychuk](https://github.com/tj) 【[Express]() / [Koa](https://github.com/koajs/koa) 框架的作者】 开发的node包管理器
> 
> **n** 安装命令：`$ sudo npm install -g n` 
> 
> 安装最新版本：`$ n latest`
> 
> 安装稳定版本：`$ n stable`
> 
> 删除某个版本：`$ n rm 0.10.1`
> 
> 其他Command命令请参考 `$ n help`

#### nvm 
> [`nvm`](https://github.com/creationix/nvm) 它与`n`的实现不同，是通过shell脚本实现的
> 
> **nvm** 安装脚本有两种方式：
> 
> `curl https://raw.github.com/creationix/nvm/v0.4.0/install.sh | sh`
>
> `wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash`
> 
> 查看可用最新版本：`$ nvm list-remote`
>
> 查看已安装的node版本：`$ nvm list`
>
> 安装版本：`$ nvm install 6.7.0`
> 
> 其他Command命令请参考 `$ nvm help`
>