##day2 NOTE
###Node全局---global
- Node下最常用的三个异步方法
	- setImmediate
	- setTimeout
	- process.nextTick  （最快）; 下一队列，重要的事情放在nextTick;
####补充
- 当判断null 和undefined时，不要采用===的写法
- console下的常用api
	- log
	- info
	- error
	- dir
	- warn
	- time
	- timeEnd
```
console.time('start');
for(var i=0;i<1000000;i++){

}
console.timeEnd('start');
```
####global上常用的属性
- progress 进程
	- process.pid 每一个进程都有一个pid号
	- process.kill(process.pid);
	- process.exit(); 退出进程
	- process.env.xxx ; 区分开发环境和生产环境，在电脑上设置变量process.env代表
	- process.nextTick 下一队列，异步;
- buffer
- clearImmediate 立即清除
- setTimeout 定时器
- setInterval 定时器
- setImmediate 立即  异步,不确定时间,如果不设置时间的话，我们会采用setImmediate;
-
```
setImmediate(function(){
	console.log('立即');
})
```

- 1、改变this方法
	- apply,函数立即执行
	- call，函数立即执行
	- bind  ：函数不立即执行，需手动执行，只能绑定一次，不能连续绑定，如果连续绑定，输出的结果是第一次绑定的
	- 缓存this，通过设置一个变量来进行缓存this，进而改变this指向
	- 箭头函数处理this，自身没有this指向，所以要向上查找，所以this是指向外层作用域的
- 2、传递参数 可以从第二个参数开始传递实参
```
setTimeout(eat,1000,'banana','apple');
```
- 3、获取参数列表
	- [].slice.call(arguments,1);
	- Array.from(arguments).slice(1),可以直接将arguments对象转化为数组
	- 可以使用省略号(剩余运算符)来获取剩余参数  ，将剩余参数转化为数组类型;
```
function eat(what,...args){//args除第一个参数外的剩余参数
	console.log（arguments）; //在Node下arguments是对象;
	console.logo(what);
}
```
- 剩余运算符在除参数外，被用作拓展运算符
```
let ary = [1,2,3];
let ary1 = [4,5,6];
console.log([...ary,...ary1]);
```


###5个特殊形参


- node基于commonjs规范的
- commonjs规范 （操作的是模块）
	- 1、如何使用模块
		- require使用模块 ，require方法同步，如果有回调函数，则肯定是异步代码
		- 模块分为：
			- 内置模块
			- 第三方模块 写模块名字即可
				- 全局的第三方模块，加了-g只能在命令行使用
					- nrm模块 默认下载模块通过npm下载，切换到国内，
					- (sudo)npm install nrm -g，安装成功后就会全局下有一个nrm命令
						-  nrm ls  列出所有源
						-  nrm test 测试源的网速
						-  nrm use 用哪个源
					- cnpm 、 taobao 源
					- 常见模块 nodeppt模块，http-server启动服务，用于调试;
				- 本地第三方  在当前文件夹下使用
					- 开发依赖 --save-dev或者-D 只是开发需要   babel、less、webpack、gulp等
					- 生产依赖 --save或者-S 开发上线都需要  jQuery、Vue、Angular、React
					- 安装之前，要先初始化，否则如果外层文件夹有node_modules的话，就会默认安装到外层同名文件夹下
						- 初始化时，路径文件夹不能有汉字，特殊符，大写，而且也不能叫下载的模块
							- npm init -y ，生成package.json文件中名字不能和包的名相同，而且不能有注释;
							- 安装包成功之后，会默认自动安装到生成的node_modules中，引入第三方时会直接在当前文件夹下的node_modules中查找;
					- 卸载模块（要和安装的时候一样，也要注明是开发依赖还是生产依赖）
						- npm uninstall 包名 --save/--save-dev
			- 自定义模块（文件模块）:引用时需要相对路径
	- 2、如何定义模块
		- 一个js文件就是一个模块
	- 3、如何导出模块
		- 首先模块是通过闭包去实现的，闭包中存在 module,exports = exports = {}; 最终闭包的返回值是module.exports
		- exports  不能批量导出
		- module.exports 可以批量导出
		- exports.a = a  ;如果使用exports导出必须通过属性添加，否则无法挂载在module.exports上
		- 想要直接导出，可以module.exports = a;
		- 也可以通过添加属性方法  ,module.exports.a = a;
		- 引入另一自定义模块的模块，接收到的结果是自定义模块导出的module.exports，只有这一个 ，而不是exports;
		- module.exports可以直接导出，也可以通过添加属性导出
		- 但是exports只能通过添加属性来导出，而不能直接导出;即所谓的exports不能批量导出，module.exports可以批量导出
		- 多次require不会多次导入，默认会缓存到require.cache这个对象中;
```
(function(){
	module.exports = exports = {};
	return module.exports;
})()

```


###自己手写一个第三方模块，发布包
- 多个模块组成一个包
- 包必须要存在package.json文件
- name:是唯一的
- main 是入口文件，默认是index.js
- 切换到NPM上
- 登陆，注册
	- npm addUser
- 发布
	- npm publish

###第三方模块引入
- 第三方模块引入的时候，会首先在当前目录下找node_modules文件夹，然后找到对应的模块，进而找到模块文件夹中的package.json，找到入口文件将其执行，如果当前目录下没有node_modules，则会向上一级目录继续查找，直到找到根路径为止;


###核心模块（内置模块）
- fs
- http
- url
- util node自带的工具包  继承inherits
	- 原生js中的继承
		- call继承  只能继承私有属性
		- 原型继承  继承私有和公有属性    缺点 不能传递参数
		- 冒充对象继承  继承公有属性 而且子类无法修改父类原型上的方法
		- es5
		- es6
	- util.inherits(childFn,parentFn); 只继承公有属性和方法;
- events  node自带一个事件库 (发布订阅模式)
	- 特点 :订阅代表 一对多的关系  ；发布，就是当事件触发后，执行所有的事情
	- 例如 {女生失恋了:[吃，哭，逛街]};
	- $emit 发布
	- $on 订阅

###http-server模块
- 帮助用户启动一个服务，返回静态文件
- 安装
	- npm install http-server -g
- 使用:在想要访问的文件夹下启动服务
	- http-server -p 3000
###nodeppt模块
- 安装
	- npm install nodeppt -g
- 使用：在想要执行的文件夹下,必须是md文件，而且文件中需要有[slide]
	- nodeppt start


>模块化是通过闭包去实现的，在Node中的每一个模块都是在一个闭包中，可以将重要的属性挂载到global上，这样全局每一个模块都可以进行访问操作

>单目运算符 + - 可以将字符串转化为数字

>AJAX只能在有域名的情况下运行，在文件夹目录下不会运行的;
```
console.log(1 -"3");  //-2  存在空格
console.log(1+ +'3'); //4 存在空格
```


###搭建静态博客 hexo
- 安装 hexo
	- npm install hexo-cil -g
- 在开发目录下初始化blog，生成blog文件夹
	- hexo init blog
- 通过cd  进入到blog目录
- 然后npm install
- 启动服务  hexo server
- 部署到github上
	- 一个帐号一生只能部署一次
	- 仓库名字：用户名+.github.io
- 发布github需要一个发布到github的插件
	- npm install hexo-deployer-git    --save-dev
	- 然后打开_config.yml配置文件进行配置;
- 发布  （每次更新博客都要进行这两部）
	- hexo g 生成
	- hexo d 发布


###yarn 包管理器 (安装之后会缓存，速度快)
- npm install yarn -g
- yarn init -y
- yarn add
- yarn add -dev
- yarn remove