##node
###global.js
- process 进程
- Buffer 缓冲区
- clearImmediate: [Function]
- clearInterval: [Function],
- clearTimeout: [Function],
- setImmediate: [Function],
- setInterval: [Function],
- setTimeout: [Function],
```
1)改变this的方法
A、改变函数中的this指向(call,apply)会导致函数执行,bind不会
B、bind只能绑定一次
C、var that = this保存this指向
D、使用箭头函数处理this，因为自己家没有this指向 
```
```
2)传递参数  可以从第二个参数开始传递实参
3)获取参数列表(将arguments转化成数组)
1.[].slice.call(arguments,1);
2.Array.from(arguments).slice()
3.剩余运算 ...args 将其他参数转换成数组类型(拓展 展开运算符)  [...arr,...arr1]

//3.setImmediate 异步 setTimeout(如果没有设置时间，我们会采用setTimeout)
setImmediate(function () {//不支持设置时间
    console.log('立即')
});
setTimeout(function () {
    console.log('setTimeout');
});



4.process进程
```
###process.js进程
```
//4、process进程
console.log(process.pid);
//process.kill(process.pid);//杀死进程
//process.exit();退出进程
setInterval(function () {
},1000);

//区分开发环境 和上线环境

//1)在电脑上设置变量 process.env 代表当前进程的环境变量
//set NODE_EVN=development【开发】
//判断条件一般都是三等号 判断null和undefined可以使用两个等号
console.log(process.env);
if(process.env.NODE_EVN === 'development'){
    console.log('开发环境');
}else{
    console.log('线上环境');
}

//2)process.nextTick 下一队列（当前队列底部）
process.nextTick(function () {
    console.log('nextTick');
});
setImmediate(function () {
    console.log('setImmediate');
});
//重要的事情放在nextTick中，稍微不重要的setImmediate

/*setInterval(function(){},100
```
##module

``
### 模块笔记
- 1.如何使用模块 require使用模块
	- 文件模块 引用是需要相对路径引用  ./../
	- 第三模块 写模块名字即可 不需要 ./../
	- 全局的第三方模块 加了-g 只能在命令行下使用
>- nrm模块 默认下载模块通过哦的是nrm下载，切换到国内cnpm tabao
>- (sudo) npm install nrm -g 安装后就会拥有为全局命令nrm
>- nrm ls 列出所有可用源 nrm test 测试源的网速
> - nodeppt模块 http-server启动服务的，可以用于调试

  -	本地第三方 在当前文件夹下使用
  > - 开发依赖 --save -dev或者 -D 只是开发时使用 例如： less labe1 webpack gulp
  > - 发布依赖 --save或者 -S 上线开发需要 例如mime
  > - 安装之前 需要初始化package.json
  >   - 初始化时不能有汉字不能用特殊符，而且也不能叫要下载的模块，不能自己安自己
  >   - 不能包含注释内容
      ```
        npm init -y
      ```
   - 卸载模块
 ```
     npm uninstall jquery  --save
 ```
 >安装文件，会默认安装到node_modules下，require的时候会自动去查找
 
 - 核心模块 内置模块
- 2.如何定义模块 在node，一个js文件就是一个模块
- 3.如何导出模块
```
exports
module.exports
```
- http -server
  - 帮用户启动一个服务，返回静态文件
  >npm install http-server -g
 
  - 在想要访问的文件下启动服务
  >http-server -p 4000

- nodeppt
	- 安装nodeppt模块
	>npm install nodeppt -g
	- 想要执行的文件夹下，文件中包含slide
	>npdeppt start
	
- 发布包 多个模板组成一个包
	- - 包必须要存在package.json文件
        >npm init -y
	
		- 切换到npm上
        > nrm use npm
	
		- 登录、注册
	    > npm addUser
	
		- 发布包
	    >npm publish
	    
- 查看占用的端口
> netstate -anto | findstr "8080"
> ps -ef | grep node
> kill pid
##pack
###路径，hello.js
```
//在当前文件夹下使用这个第三方模块
let result = require('hansome-boy');
//1.第三方模块会到当前目录下找node_modules,找名字叫handsame-boy,找到后找到对应package.json,找到入口
console.log(module.paths);//查看路径
```
###继承公有属性和继承私有属性，core.js
```
//核心模块 node自带的模块，fs http url...
//util 工具包node自带的工具包 继承inherits
//
//1.call
function Parent() {
    this.cardId = 'xxx123123'
}
Parent.prototype.eat = function () {
    console.log('吃肉');
};
function Child() {
    let util = require('util');
    util.inherits(Child,Parent);//只继承公有属性
    console.log(uitl.isArray([]));
    console.log(util.isFunction([]));
}
//typeof instanceof Object.prototype.toString.call();
//返回的是boolean类型


// events node 自带一个事件库（发布订阅模式）
//发布订阅 最常见的两个方法  on emit




//5)继承公有  Object.setPrototypeof()  es6的
/*
Object.setPrototypeOf(Child.prototype,Parent.prototype);
let child = new Child();
*/


//4)j继承公有 es5的
/*
function create(parentPro) {
    let Func = function () {};
    Func.prototype = parentPro;
    return new Func();
}
Child.prototype = create(Parent.prototype);
*/

//3)继承公有  的属性     利用原型链__proto__
//Child.prototype.__proto__ =Parent.prototype;

//2).new Parent 不能传递参数 （继承私有 也继承公有）
//Child.prototype = new Parent();

//1).call继承（只继承私有）
//在儿子类中执行Parent方法并且让this指向儿子
/*
function Child() {
    //Parent.call(this);
}
let child = new Child();
child.eat();
*/
```
##events
###events .js   (on,emit)
```
// events node 自带一个事件库（发布订阅模式）
//发布订阅 最常见的两个方法  on emit


/*

发布订阅,最常见的两个方法 on emit
发布订阅模式，订阅代表的就是一对多的关系，发布，就是当事情触发后，执行所有的事情

{女生失恋了:[吃,逛街,哭]}

*/


function Girl() {
    this._events = {} ;   //私有属性
}

//{'女孩失恋了':[cry,eat,shopping]}
Girl.prototype.on = function (eventName,callback) {
    //先判断是否有这个对象
    if(this._events[eventName]){//第二次  有事件了就开始添加事件
        this._events[eventName].push(callback);
    }else {//第一次  也就说刚开始时没有，需要创建一个事件
        this._events[eventName] = [callback]; //arr
        //{ '女孩失恋了':[cry]}
    }
};


Girl.prototype.emit = function (eventName,...others) {//others 代表除了第一个的参数数组
    if(this._events[eventName]){
        this._events[eventName].forEach(item=>{
            item.apply(this,others);  //如何将数组中的每一个依次传入到函数中
            /*apply:方法能劫持另外一个对象的方法，继承另外一个对象的属性 */
            item.call(this,...others); //...others展开运算符将数组整个展开
        });//forEach的第二个参数是this指向
    }
};

Girl.prototype.removeListener = function (eventName,callback) {
  if(this._events[eventName]){ //filter过滤返回新数组，如果函数中返回true添加到新数组中，返回false，这项就不要了
      this._events[eventName]=this._events[eventName].filter(item=>{
          return item !==callback;//返回true留下 返回false丢掉
      });

  }
};
let  girl = new Girl();

function cry(who,who1) {console.log('大哭'+who+who1);}
function eat(who,who1) {console.log('吃'+who+who1);}
function shopping(who,who1) {console.log('购物'+who+who1);}

girl.on('女孩失恋了',cry);
girl.on('女孩失恋了',eat);
girl.on('女孩失恋了',shopping);

girl.removeListenter('女孩失恋了',shopping);

girl.emit('女孩失恋了','我','你'); //会让cry eat shopping依次执行
```
###2.events.js (util)
```
let EventEmitter = required('events');
let util = required('url');
function Girl() {}
util.inherits(Girl,EventEmitter);//node写法 继承 与events一样
let  girl = new Girl();

function cry(who) {console.log('大哭'+who);}
function eat(who) {console.log('吃'+who);}
function shopping(who) {console.log('购物'+who);}

girl.once('女孩失恋了',cry);//只执行一次

girl.on('女孩失恋了',cry);
girl.on('女孩失恋了',eat);
girl.on('女孩失恋了',shopping);

girl.removeListenter('女孩失恋了',shopping);//移除事件

girl.emit('女孩失恋了','我'); //会让cry eat shopping依次执行
girl.emit('女孩失恋了','我'); //会让cry eat shopping依次执行
//绑定 发射 移除 绑定一次  删除全部
//on=addListener emit removeLister once removeAllisters
```
## 搭建静态博客hexo
- 安装hexo模块
```  
npm install hexo-cli -g 
```

- 生成博客项目
```
 hexo init blog
```
 
-  进入目录安装依赖
```
cd blog && npm install
```

- 启动服务
```
hexo server
```

##部署到github上
  - 一个账号只能部署一个,名字必须交 用户名.github.io

##发布github需要一个发布到github的插件
```
npm install hexo-deployer-git --save
```
## 配置发布文件
```
deploy:
  type: git
  repo: https://username:password@github.com/zuyuan/zuyuan.github.io.git
  branch: master
```
## 发布
- 当前目录下,每次更新都需要执行这两部
```
hexo g 生成
hexo d 发布
```
## yarn包管理器

 - 相当于你把nrm use cnpm,支持缓存
```
npm install yarn -g
```
##yarn
- 安装yarn
```
npm install yarn -g
```
- 初始化package.json
```
yarn init -y
yarn add jquery vue 
yarn add babel-core -dev
```