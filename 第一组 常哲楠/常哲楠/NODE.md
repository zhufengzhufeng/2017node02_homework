#NODE
[toc]
>node是一个服务端运行js的环境，是一门服务端语言。
##基础
###前端模块化
模块化是一种开发规范，比如cmd，amd是为了更好的解耦。

前端的模块化实现方式
- 闭包
- 单例：不能完全解决命名冲突；调用时代码过长的问题
- requirejs(amd)依赖前置
- seajs(cmd)就近依赖


###node特点

node的特点：
- 异步i/o，常见的定时器，回调
- 单线程，其他语言都是多线程的，多线程实现就是切换执行上下文
- 进程：进程包括线程，node一个进程只能开一个线程


##全局对象(global)
这部分笔记参考课上笔记加[菜鸟教程](http://www.runoob.com/nodejs/nodejs-global-object.html)

JavaScript 中有一个特殊的对象，称为全局对象（Global Object），它及其所有属性都可以在程序的任何地方访问，即全局变量。
在浏览器 JavaScript 中，通常 window 是全局对象， 而 Node.js 中的全局对象是 global，所有全局变量（除了 global 本身以外）都是 global 对象的属性。
在 Node.js 我们可以直接访问到 global 的属性，而不需要在应用中包含它。

全局对象与全局变量
global 最根本的作用是作为全局变量的宿主。按照 ECMAScript 的定义，满足以下条 件的变量是全局变量：
- 在最外层定义的变量；
- 全局对象的属性；
- 隐式定义的变量(未定义直接赋值的变量)

当你定义一个全局变量时，这个变量同时也会成为全局对象的属性，反之亦然。需要注意的是，在node.js不可以在最外层定义变量，因为所有用户代码都是属性当前模块的，而模块本身不是最外层的上下文
**注意**定义变量时要使用`var/let`关键字，避免引入全局变量，因为全局变量会污染命名空间，提高代码的耦合风险。


如果去打印出全局对象
```
console.log(this);//如果是在全局中，打印出的是module.exports对象

//但如果是在闭包中打印就可以获得global对象
(function () {
	console.log(this);//-->global
})();
```

在全局对象上有几个重要的属性

###process
process是一个全局变量，即global对象的属性。
它用于描述当前Node.js进程状态的对象，提供了一个与操作系统的简单接口。通常在写本地命令程序的时候使用

在webstorm中，使用Node运行完代码后会在最后显示
```
//状态码为0的正常退出
Process finished with exit code 0
```

####pid
表示当前进程的进程号。
可以设置一个循环，显示当前的进程号
```
console.log(process.pid);
setInterval(function () {

}, 1000);
```
可以在电脑的任务管理器-->详细信息查找到这个进程号，并关掉，这时命令行里
```
Process finished with exit code 1
```

可以使用代码挂掉
```
process.kill(进程号);
```

如果想正常即出
```
process.exit();
```

####env
返回一个对象，成员为当前 shell 的环境变量。
在电脑上设置变量
cmd
```
//等号间不要有空格
set NODE_EVN=development
```

代码
```
if (process.env.NODE_EVN === 'development') {
	console.log('开发环境');
} else {
	console.log('线上环境');
}
```

cmd
```
node 文件名
//输出开发环境
```

####nextTick
下一个队列，异步
对比
永远是process.nextTick最快
- process.nextTick()
- setImmediate()
- setTimeout()

所以最重要的事件要使用process.nextTick，次重要的事件放到setImmediate里

###定时器
clearImmediate清除立即
setImmediate设置立即
setTimeout
setInterval
clearTimeout
clearInterval

####this问题
如引输出的this是定时器本身
```
setTimeout(function () {
	console.log(this);
}, 1000);
```

但是使用箭头函数的话，就是指向外层的this，即module.exports
```
setTimeout(() => {
	console.log(this);
}, 1000);
```

如果想修改定时器中的this为obj对象(function写法)
```
//this还是定时器
let obj = {
	a: function () {
		setTimeout(function () {
			console.log(this);
		}, 1000);
	}
};

obj.a();
```

方法1：缓存this
```
let obj = {
	a: function () {
		let _this = this;
		setTimeout(function () {
			console.log(_this);
		}, 1000);
	}
};

obj.a();
```
方法2：使用bind
```
let obj = {
	a: function () {
		setTimeout(function () {
			console.log(this);
		}.bind(this), 1000);
	}
};

obj.a();
```
方法3：箭头函数
```
let obj = {
	a: function () {
	    setTimeout(() => {
			console.log(this);
	    });
	}
};

obj.a();
```

####定时器时间问题
对比
- setTimeout()不写时间
- setImmediate()
- process.nextTick

setImmediate是立即执行，但是是异步，它不识别放置的时候，表示回调立即执行。和setTimeout不设置时间的相比，哪个先执行具有不确定性。

但是这两个都比process.nextTick后执行

###console

log
info
dir
error
warn

可以计算时间差
开始和结束的名字必须相同，否则会报错
- time
- timeEnd

```
console.time('start');
for (let i = 0; i < 100000000; i++) {

}
console.timeEnd('start');
```



###buffer

###__filename


###__dirname


##模块化
每个文件都是一个模块，模块化是通过闭包实现的

###如何使用模块
使用`require`就可以引入一个模块
对于三种模块有自己的引入方式
- 文件模块：自己写的模块，引用时需要加上相对路径
- 第三方模块：其他人写的文件，引用时直接使用模块名，不需要路径
- 核心模块：内置模块。引用时直接使用模块名，不需要路径

下载第三方模块
默认下载模块使用npm，下载速度比较慢，如果想切到国内，那么需要一个nrm，安装之后就可以使用cnpm或者taoabo等国内镜像。
```
//全局安装
npm install nrm -g

//列出所有可用源
nrm ls
* npm ---- https://registry.npmjs.org/
  cnpm --- http://r.cnpmjs.org/
  taobao - https://registry.npm.taobao.org/

//想测试哪个速度快
nrm test
* npm ---- 907ms
  cnpm --- 360ms
  taobao - Fetch Error

//指定下载源
nrm use taobao
```

一些好玩的模块
- nodeppt：
	- 在目录下使用`nodeppt start`
	- 只支持md
	- 文件中要包含`[slide]`
- http-server，可以用于调试移动端的项目
	- 帮用户启动一个服务，返回静态文件
	- 在想要访问的文件夹下启动服务
	- 加`-p`可以指定下端口号


开发/代码依赖
- 全局的第三方模块`-g`只能在命令行里使用，不可以在代码里使用
- 本地第三方模块：在当前文件夹下使用。使用之前先配置package.json。如果外层文件有`node_module`就会向上安装。初始化`npm init -y`
	- 开发依赖`--save-dev/-D`只是开发时使用，例如less babel webpack gulp
	- 代码/发布依赖`--save/-S`上线开发全需要，例如vue mime 

###如何定义模块
一个js文件就是一个模块

如何在npm上创建一个自己的包
多个模块组成一个包
1. 这个包必须要存在`package.json`文件
```
npm init -y
```
2. 必须有`index.js`
3. 登录或注册`npm addUser`
	- 会要求写名字和密码和邮箱
	- 出现logged in就可以了
4. 切到npm上(国外npm)`nrm use npm`
5. 发布包，`npm publish`




###如何导出模块
导出的模块就是this指针的指向，导出的模块永远是`module.exports`对象
导出方式：
- exports：如果使用这个就得使用属性添加，否则就无法挂载到`module.exports上`
- module.exports：这个是导出的对象，因此可以重写这个对象，而无须往上挂载属性

大致的原理
```
(function () {
    this = module.exports;
    module.exports = exports = {};
    ...
	return module.exports;
})();
```

##核心模块

###util
util是node自带的工具包

####inherits
继承，只继承公有属性
```
let util = require('util');

function Parent() {
	this.cardId = 'xxx123123';
}

Parent.prototype.eat = function () {
	console.log('吃肉');
};

function Child() {

}

util.inherits(Child, Parent);
```

####判断
- isArray判断对象是否为数组类型
- isDate判断对象是否为日期类型
- isRegExp判断对象是否为正则类型


###events

自带了一个事件库，发布订阅模式
发布订阅最常见的两方法on emit
- 订阅就是一对多的关系
- 发布就是当事件触发后执行所有事件

原生写法
```
//发布和订阅

//原生发布订阅
function Girl() {
	this._events = {};
}

Girl.prototype.on = function (eventName, callback) {

	if (this._events[eventName]) {
		//第二次以后
		this._events[eventName].push(callback);
	} else {
		//第一次
		this._events[eventName] = [callback];
	}
};

Girl.prototype.emit = function (eventName, ...others) {
	//others代表除第一项外的参数，是一个数组
	if (this._events[eventName]) {
		this._events[eventName].forEach(item => item.apply(this, others));
	}
};

Girl.prototype.removeListener = function (eventName, callback) {
	if (this._events[eventName]) {
		this._events[eventName] = this._events[eventName].filter(item => item !== callback);
	}
};

let girl = new Girl();

function cry(who) {
	console.log(who + 'cry');
}

function eat(who) {
	console.log(who + 'eat');
}

function shopping(who) {
	console.log(who + 'shopping');
}

girl.on('失恋', cry);
girl.on('失恋', eat);
girl.on('失恋', shopping);

girl.removeListener('失恋', shopping);

girl.emit('失恋', 'I ');//会让绑定的三个方法执行
```

使用events模块的发布订阅
```
let EventEmitter = require('events');
let util = require('util');

function Girl() {}

util.inherits(Girl, EventEmitter);

let girl = new Girl();

function cry(who) {console.log(who + 'cry');}

function eat(who) {console.log(who + 'eat');}

function shopping(who) {console.log(who + 'shopping');}

girl.on('失恋', cry);
girl.on('失恋', eat);
girl.on('失恋', shopping);

girl.removeListener('失恋', shopping);

girl.emit('失恋', 'I ');//会让绑定的三个方法执行
girl.emit('失恋', 'I ');//再次会让绑定的三个方法执行
```

如果只想触发一次的话可以使用
```
girl.once('')
```
删除所有
```
removeAllListeners
```



###fs




###http





###url




##如何搭建静态博客
[HEXO](https://hexo.io/)

```
//安装模块
npm install hexo-cli -g
//项目文件夹
hexo init blog
cd blog
npm install
hexo server
```

布署到github上
一个账号只能布署一个
因为仓库名只能是
```
//用户名 + github + io
Joo-fanChang.github.io
```
还需要一个插件：`npm install hexo-deployer-git --save`

文件
`_config.yml`
最下面
注意空格和缩进，必须和原文件上的一样
```
deploy:
  type: git
  repo: https://(这里要写成用户名+冒号+密码+@)github.com/Joo-fanChang/Joo-fanChang.github.io.git
  branch: master
```

发布命令：
```
hexo g 生成
hexo d 发布
```
之后每次都得，执行这两步操作


##yarn包管理器
```
npm yarn -g
```

```
初始化
yarn init -y
安装
默认加--save，但不是会默认加-dev
yarn add jquery@3.0.0 vue 
yarn remove jquery
```