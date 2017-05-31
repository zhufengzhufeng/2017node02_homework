###正式课第十周第五天
####global属性
- console time timeEnd 可以计算时间差
```
console.time('start');
for(let i=0 ;i<1000;i++){};
console.timeEnd('start');
```
- setTimeout中的this问题
```
/*1.改变this的方法，在回调函数后加bind(this),bind只能绑定一次
*2. var that =this,保存this指向
*3.使用箭头函数处理this，因为自己家没有this指向，从而解决了this问题
*/
setTimeout(function(){
	console.log(this);//代表计时器自己，不是global
})；
/*传递参数 可以从第二个参数开始传递实参
*
*/
function eat(what，what1,what2){
//获得除了第一个参数后面的所有参数
1.let args=[].slice.call(arguments,1);
2.let args1=Array.from(arguments).slice(1);
3.剩余运算符...args 将其他参数转换成数组类型
4.拓展运算符...(课后)
console.log(what,what1,what2);
console.log();
};
setTimeout(eat,1000,"香蕉","apple","橘子");
```
- setImmediate 异步
```
/*不支持设置时间，如果没有设置时间，我们会采用setImmediate
*/
setImmediate(function(){
	console.log("立即");
});
```

- process进程
```
console.log(process.pid)
process.kill(process.pid);
process.exit();
/*区分开发环境和上线环境：
*在电脑上设置环境变量 ，mac本上不需要加set
*/
set NODE_EVN=development;
if(process.env.NODE_EVN==='development'){
	console.log('开发环境');
}else {
	console.log('线上环境');
}
setInverval(function(){},100);
2. process.nextTick() 下一队列,执行速度是最快的，重要的事情放在nextTick中 
```
####五个特殊的变量
1. node基于commonjs（模块）规范的
> 如何定义模块：在node中一个js文件就是一个模块
>  如何使用模块：
>  1. 文件模块，引用时需要相对路径引用 ，第三方模块，核心模块,直接引用。
>  2. require方法是同步的，如果有callback的都是异步方法，返回的是{}
>  3. 每个文件都是一个模块，模块化是通过闭包实现的
>  4. 如果使用exports导出必须通过属性添加，否则无法挂载在module.exports上，返回的是module.exports，所以可以直接改变module.exports的指针
>  5. 全局的第三方模块，加了-g只能在命令行下使用。默认下载模块是npm下载，切换到国内nrm下载
>  6. 本地第三方 ，在当前文件夹下使用的。开发依赖：--save--dev/-D，只是开发时使用，例如：less，babel, webpack,gulp;    发布依赖:--save/-S,例如mime。安装之前需要初始化package.json
	- 初始化时不能有汉子不能用特殊符，而且也不能叫要下载的模块
	- npm init -y
	- npm install mime --save-dev
	- npm uninstall mime --save-dev
```
(sudo) npm install nrm -g
//安装玩以后就会拥有全局命令nrm
nrm ls //列出所有可用原
nrm test //测试源的网速
nrm use//用哪个源
nodeppt模块
http-serveer启动服务的，可以用于调试
```
####http-server
- 帮用户启动一个服务，返回静态文件
```
npm install http-server -g

```
- 在想要访问的文件夹下启动服务
```
http-server -p 3000
```
####nodeppt 模块
```
npm install nodeppt -g
```
- 在想要执行的文件夹下，文件中包含
```
nodeppt start
```
####发布包 ：多个模块组成一个包
- 包必须要存在package.json 文件
```
npm init -y
npm addUser//登录
npm publish//在发布包的根目录下发布
```

```
 netstat -anto | findstr "8080"//查看占用接口的程序
```
####核心模块
1. 核心模块包括：fs，http，url....
2. util工具包是node自带的工具包
3. 继承：Object.setPrototypeOf();
```
let util=require("util");
util.inherits(Child,Parent);//只继承公有属性
```
4. events node自带的一个事件库（发布订阅事件）
- 发布和订阅最常见的两个方法：emit on 
- 发布订阅模式，订阅代表的是一对多的关系，发布就是当事情触发执行所有的事情

####搭建静态博客hexo
```
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
部署到github上
```
一个账号只能部署一个，名字必须叫 用户名.github.io
```
发布github需要一个发布到github的插件
```
npm install hexo-deployer-git --save
```
配置发布文件
```
deploy:
  type: git
  repo: https://username:password@github.com/zuyuan/zuyuan.github.io.git
  branch: master
```
发布
- 当前目录下
```
hexo g//生成
hexo d//发布
```