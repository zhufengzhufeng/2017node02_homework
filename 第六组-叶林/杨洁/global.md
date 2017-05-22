## 全局对象global和五个特殊形参
[toc]
### global
- node中没有window属性
```
- console.log(this); // {}   不是global
```
- 定时器中的this是定时器自己
```
set timeout(function(){console.log(this)});

```
- 闭包中的this才是global
```
~function(){console.log(this)}; //global
```
- 小细节
    1. var 不能直接将内容挂载在global上
    2. let const只要内存地址不变是可以改变内容
    3. 同一个作用域{}下变量不能声明两次
    4. 使用{}必须要写retrun

### global中的一些属性
- process
- Buffer
- clearImmediate: [Function] 清除立即
- clearInterval: [Function]
- clearTimeout: [Function]
- setImmediate: [Function]
- setInterval: [Function]
- setTimeout: [Function]
- console: [Getter] } log info dir error warn time timeEnd

### console time timeEnd可以计算时间差
```
console.time('start');
for(let i = 0; i<100;i++){}
console.timeEnd('start');
```
### setTimeout setInterval (this代表的是定时器自己)
1. 改变this的值
> - 改变函数中的this指向(call,apply)会导致函数执行
> - bind只能绑定一次
> - vat that = this保存this指向
> - 使用箭头函数处理this，因为自己家没有this指向 从而解决了this问题.

---
 2.传递参数 可以从第二个参数开始传递实参
 ```
1.[].slice.call(arguments,1);
2.Array.from(arguments).slice(1); 
3.剩余运算 ...args 将其他参数转换成数组类型 （拓展 展开运算符） [...arr,...arr1]
function eat(what,...args) { //arguments(实参的集合)
 ```
 3.获取参数列表(将arguments转化成数组)

### 配置环境变量
- node可以在命令行下执行的原因
- 将可执行文件配置到了环境变量下
> 系统->属性->高级系统设置->环境变量->path->新增即可
### 前端的模块化：
- 闭包
- 单例(有且只有一份): 不能完全解决命名冲突，调用时代码过长
- requirejs(AMD)依赖前置 seajs(CMD)就近依赖
- commonjs 规范，是node模块的实现 module.exports

### node特点
- 异步io （定时器,回调函数）
- 单线程(其他语言多线程) 多线程实现就是切换执行上下文(速度很快感觉不出来，好像在干很多件事)
- 进程是包含线程的，node一个进程只能开一个线程

### 事件环 
- 靠事件驱动的


