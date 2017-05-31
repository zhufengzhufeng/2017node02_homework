#git

mac安装 brew

git config --list //查看配置项
git  config --global user.name XXX
git  config --global user.email XXX

mkidir   cd

git init

touch  创建

ls   查看

cat   打开文件

vi  编辑 

esc +:wq

git add 加入暂存区

git   commit -m


git status   //查看git 状态红色表示没有在暂存区   绿色表示在暂存区中    

git commit  -m 'jjj'
git log   --oneLine


git  diff   +文件名 工作区 和暂存区
git diff --cahced  暂存区 和历史
git diff --master 工作区 和历史区

回滚  把暂存区 覆盖  工作区

git status

git  checkout .  +文件名或者 .

历史区有版本号  
选择某个版本进行回滚操作  
把历史区 覆盖  工作区
commit 后面最少7位
git  reset --hard id


git  reflog

创建 gitignore 必须在


删除上一次 添加暂存区的内容  变成上一次
git branch  查看分支
git branch  +分支名 建立分支
创建的分支 和 master 一样   

git checkout +分支名

git  -D +分支名  删除分支
 git branch -D dev

将内容提交到某个分支上   默认我们的代码放在工作区上 不属于任何分支  只



主干没有任何更新  
git merge dev
Updating cc52f20..57aa6ef
Fast-forward

 git merge dev

手动删除不要的

git commit -a -m 'merge'

mac  oh my zsh
item2


git  hub  是commit  结果 历史区


echo  写内容到文件  >  >>是追加

本地与线上版本不一致
线上版本新
线下
git push origin master -u  省略 用户名密码
git pull origin master 获取最新代码

冲突 手动解决
推送之前先拉取  

部署git 静态网页
将网页通过git 网址访问 只能放静态页  不能放置server

第一步  
需要一个分支   (gh-pages )
将代码提交到这个分支上  未提交过的要git  add  git commit  git push
推送到github上 将gh-pages 提交到这个分支上
在github 中setting上可以找

代码 合并请求管理提交的笔记

叉子 将别人的代码 当前的状态 克隆一份放到自己的仓库上  一个项目只能 fork一次 我的代码更新不会导致你的项目更新

clone 地址  文件别名
克隆将线上的项目 拉取到本地  拉下来就是git 仓库而且添加内容
git add
git commit -m
git push origin master


组员提交给自己

clone
克隆将线上的项目 拉取到本地  拉下来就是git 仓库而且添加内容
git add
git commit -m
git remote add leader  组长的地址 建立一次即可
git pull leader master
git push origin master

组长再次提交给老师

将自己的内容放进去
git add .
git commit -m 'team xxx'
git remote add teacher https://github.com/zhufengzhufeng/2017node02_homework
git pull teacher master
git push origin master



#node

配置环境变量
node可以在命令行下执行的原因
将可执行文件配置到了环境变量下

单例  

requirejs AMD 依赖前置
seajs  CMD  就近依赖
commonjs  规范 是node模块的实现 module.exports

特点
异步io (定时器 回调函数)
单线程(其他语言多线程)
多线程的实现 是切换执行环境  执行上下文 速度很快感觉不出来 
进程  包含多个线程   node一个进程 只能开一个线程

如何解决异步问题?回调函数   当我们调用read 方法时传入后续的逻辑函数作为参数

node 事件驱动  事件环  靠事件驱动   
全局对象
global 在当前文件夹下直接使用的都是全局对象
全局对象 global 上的属性 + 五个特殊的形参
node上没有window
this. 是{}空对象
闭包  里的this  是golbal

**定时器里的this 是自己 **

var  不能直接将变量挂载在global上
没有var 声明的会挂载在global上  写代码不要丢let const
const  引用类型 不改变地址 不会报错
同一个作用域下变量不能声明两次
作用域 就是{ }

arrow func  
如果使用了{} 必须写return
let sum = (a,b) => a+b;

```
 function a(a) {
        return function (b) {
            return a+b
        }
    }
    等同于
    let a=a =>b=>a+b;
```


#day2
global
process 进程
 buffer  缓存区
 clearImmediate
clearInterval
clearTimeout
setImmdiate
setInterval
setTimeout
console
```
console.time('start');
for(let i=0; i<1000;i++){}
console.timeEnd('start');


改变函数中的this  指向  (call apply)会导致函数执行
function a() {
    console.log(this);
}
var fn=a.bind(1).bind(2)  //1   bind只能绑定一次
```

let obj ={
    a:function () {
        let that = this;
        setTimeout(()=>{
            console.log(this);
        },1000)
    }
}
obj.a();

function eat(what) {

}
setTimeout(eat,1000,'香蕉')

//传递参数 可以从第二个参数开始传递参数


// setTimeout(eat.bind(null,'香蕉'),1000)
// setTimeout(function () {
//     eat('jjj')
// },1000)

//获取参数列表 剩余运算也叫拓展运算 展开 ...args 将其他参数转化数组类型
function eat(what,what1,what2) {
    let args=Array.from(arguments).slice(1);
}

function eat(what,...args) {

}

let arr=[4,5,6]

let arr1=[7,8,9]


let newarr=[...arr,...arr1];


//setImmediate  如果没有设定时间


setImmediate(function () {
    console.log('立即');
})



//process

console.log(process.pid);
setImmediate(function () {

},1000)

// process.kill(process.pid) //杀死进程
// process.exit(process.pid) //退出进程


//区分开发环境  和 上线环境
//在电脑上设置变量

if(process.env.NODE_EVN === 'development'){  //线上环境没有env.NODE_EVN这个变量  本地开发有这个变量
    console.log('开发环境');
}else{
    console.log('线上环境');
}
//cmd  node +文件名
process.nextTick(
    function () {
        console.log('next');
    }
) //下一队列(当前队列底部) 重要的事情放在nexttick 中  稍微不重要的setImmediate


/node基于commonjs 规范的
// 如何使用模块 文件模块  引用时需要相对路径 ./    第三方模块  核心模块   写文件名即可  require方法是同步的 如果有callback有回调函数的是异步 模块化是通过闭包实现的

// 如何定义模块  一个js文件就是一个模块
// 如何导出模块

(function () {

    module.exports=exports={}  //如果使用exports导出必须通过属性添加 ,否则无法挂载到moudule.exports this=moudle.exports
    return module.exports
})()


let result=require('./a.js');

console.log(result.calc['+'](40, 44));
console.log(result.calc['*'](40, 44));

//多次require 不会多次导入 默认会缓存到require.cache 这个对象中
// 全局的第三方模块 加了-g只能在命令行下使用
//nrm模块 默认是npm下载  切换到国内   npm install nrm -g   nrm ls 列出所有可用源    nrm test  测试源的网速 nrm use
//nodeppt  http-server
//npm install http-server -g
//http-server -p 3000

//npm install nodeppt -g
//nodeppt start

//本地第三方    在当前文件夹下使用
--sava--dev 或者 -D
--sava 或者 -S

安装之前要 初始化  package.json   没初始化会:如果外层有node_moudules 会向上安装  
npm init  初始化时不能有汉字 不能用特殊符  

npm uninstall --save    卸载 模块   怎么安装怎么卸载

发布包
npm init -y
nrm use npm
npm  addUser
login
npm whoami
npm publish +包名


cmd    netstat -anto|findstr '8080'  查看占用的端口  ps -ef | grep

第三方模块会到当前目录下找 node+moudule 找到对应package.json 找到入口文件将其执行,如果当前目录下没有找到,会到上一级目录查找 找到根路径为止没找到 则报错

```
原生js中有哪些继承方式？
//1.call
function Parent() {
    this.cardId = 'xxx123123'
}
Parent.prototype.eat  = function () {
    console.log('吃肉');
};
function Child() {}
let util = require('util');
util.inherits(Child,Parent);//只继承公有属性
console.log(util.isArray([]));
console.log(util.isFunction([]));
//typeof instanceof Object.prototype.toString.call();
//返回的是boolean类型





// 5.继承公有 Object.setPrototypeOf() es6的
// Object.setPrototypeOf(Child.prototype,Parent.prototype);
// let child = new Child();
// 4.继承公有 es5的
// function create(parentPro) {
//     let Func = function () {};
//     Func.prototype = parentPro;
//     return new Func();
// }
// Child.prototype = create(Parent.prototype); //儿子的原型只有父类的公有属性
// 3.继承公有
// Child.prototype.__proto__ = Parent.prototype;
// 2.new Parent不能传递参数 （继承私有 也继承公有）
// Child.prototype = new Parent();
// 1.call继承（只继承私有）
// 在儿子类中执行Parent方法并且让this指向儿子
// function Child() {
//     //Parent.call(this);
// }
// let child = new Child();
// child.eat();
```

核心模块 node 自带的模块 fs http url 
util  工具包  inherit  继承

Object.setPrototypeOf (child.prototype,Parent.prototype)

## events node自带一个事件库 (发布订阅模式)
- 发布订阅,最常见的两个方法 on emit
- 发布订阅模式，订阅代表的就是一对多的关系，发布，就是当事情触发后，执行所有的事情

{女生失恋了:[吃,逛街,哭]}

```
let EventEmitter = require('events');
let util = require('util');
function Girl() {}
util.inherits(Girl,EventEmitter);
let girl = new Girl();
function cry(who) {console.log('大哭'+who);}
function eat(who) {console.log('吃'+who);}
function shopping(who) {console.log('购物'+who);}
girl.once('女孩失恋了',cry);
girl.on('女孩失恋了',eat);
girl.on('女孩失恋了',shopping);
girl.removeListener('女孩失恋了',shopping);
girl.emit('女孩失恋了','我'); //会让cry eat shopping依次执行
girl.emit('女孩失恋了','我'); //会让cry eat shopping依次执行
//绑定  发射  移除 绑定一次  删除全部
// on=addListener emit removeListener once removeAllListeners
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
- 进入目录安装依赖
```
cd blog && npm install
```
- 启动服务
```
hexo server
```
## 部署到github上
- 一个账号只能部署一个,名字必须交 用户名.github.io

## 发布github需要一个发布到github的插件
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

## 安装yarn
```
npm install yarn -g
```

## 初始化package.json
```
yarn init -y
yarn add jquery vue 
yarn add babel-core -dev
```
