####GIT
###创建目录
```
mkdir 目录名称   创建一个新的文件夹
```
###进入目录
```
cd 目录名称    
```
###创建并进入目录
```
mkdir 目录名称 && cd 目录名称
```
###初始化git仓库
```
git init   ----- 初始化

ls -al   ----- 查看所有文件，包括隐藏文件
```
###创建文件
```
touch 文件名(带扩展名)
```
###查看文件内容
```
cat 文件名(带扩展名)
```
###编辑文件内容 
```
vi 文件名(带扩展名)
```
####vi 常用命令
```
i    -----插入
esc :wq    -----保存并退出
```
###查看git状态
```
git status
```
- 红色 表示没有在暂存区中
- 绿色 表示在暂存区中

####加入暂存区
```
git add .
```
####加入历史区
```
git commit -m 'init commit'
```
###查看历史
```
git log --oneline
```
###不同区的代码比较
```
git diff    默认是工作区和暂存区进行比较

git diff --cached     比较暂存区和历史区

git diff master    比较工作区和历史区
```
###用暂存区的内容覆盖工作区的
```
git checkout 文件名
git checkout .
```
###选择某个版本进行回滚操作 --- 用历史区想要的内容覆盖掉工作区的
```
git reset --hard 想得到的内容对应的版本号(最少截取7位)
```
###查看所有历史版本
```
git reflog
```
##创建gitignore必须在add之前创建
```
// 一般会忽略掉的文件：
.idea
node_modules
.DS_Stroe    -----mac下的
```
###删除上一次添加到暂存区的内容
```
git reset HEAD 文件名
git reset HEAD .
```




##CLI  command-line interface，命令行界面    GUI

##webstorm破解码
http://idea.iteblog.com/key.php


##git分支管理
###查看git分支
```
git branch
```
> git有一个默认自带的分支：master
###建立分支
```
git branch 分支名
```
> 创建新的分支之前，先要在master里提交个内容文件等，让master成为主干分支，再创建，最终合并分支的时候是合并到master里
> 创建的分支和master一样
###切换分支
```
git checkout 分支名
```
###删除分支
> 前提是没有在当前要删除的分支中，即需要切换到别的分支
```
git branch -D 分支名
```
###创建并切换分支
```
git checkout -b 分支名
```
###将内容提交到某个分支上
> 默认不提交的时候 代码文件等内容是在工作区上，不属于任何分支，只有提交到某个分支上，此文件才归属于特定的分支(在其他分支看不到提交以后的文件)
```
//在想要提交到的当前分支中,进行提交
git add .
git commit -m 'add'
```
###合并分支
####fast-forward
- 主干master没有任何更新
- 分支提交了新的代码
> 将主干的指针快速指向到分支最新的代码
```
git checkout master    //第一步进入到master主干里
git merge 要合并的分支名  
```
#### 合并
- 主干有更新
- 分支也有更新

```
git merge 要合并的分支名     //第一步合并
git commit -a -m 'merge'    //第二步提交

```

####conflict 合并冲突处理
- 合并多个分支时可能合并的内容会产生冲突
- 手动解决冲突(把文件里冲突的无用内容删掉)，再提交

###对于以前提交过的文件 可以一步到位提交
```
git commit -a -m 'write huge'
```

###创建有内容的文件
```
echo "# 文件内容" > 文件名  //覆盖原有
echo "# 文件内容" >> 文件名  //追加内容
```


## 提交到远程仓库
### 建立文件
- README.md
- .gitignore    可忽略文件

### 提交到历史区
- git add      到暂存区
- git commit -m '信息'    到历史区

## 查看远程仓库
```
git remote -v      查看关联
git remote add 地址的别名 地址    建立联系
git push origin master 将master推送到origin上  
```

## 本地和线上版本不一致
- 线上比线下的版本新
- 线上和线下两个版本都不一致


## 拉取最新代码
- 将线上最新代码拉取到master分支上
```
git pull origin master 获取最新代码
```

## 部署git静态网页
- 将网页通过git网址访问（只能放静态页，不能放置server）
### 第一步
- 需要一个特定的分支（gh-pages）
```
git checkout -b gh-pages
```
- 将代码提交到这个分支上
```
git add ```
git commit -m'static'
```
- 建立本地和远程的链接
```
git remote add 别名 地址
```
- 推送到github上,将gh-pages提交到这个分支上
```
git push origin gh-pages
```
- 在github中的setting上可以找到这个网址

## 代码合并请求管理提交的笔记

### fork
- 叉子，将别人的代码当前的状态，克隆一份放到自己的仓库上，一个项目只能fork一次，我的代码更新不会导致你的项目更新

### clone
- 克隆是将线上的项目拉取到本地，拉下来后就是git仓库，而且已经添加好了远程仓库地址
```
git clone 地址 文件夹名字
```

### 组长提交信息
```
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git push origin master
```

## 组员给提交给自己
```
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git remote add leader 组长的地址（建立一次即可）
git pull leader master
git push origin master
```

## 组长再次提交给老师
```
将自己的内容放进去
git add .
git commit -m 'team xxx'
git remote add teacher https://github.com/zhufengzhufeng/2017node02_homework
git pull teacher master
git push origin master
```

##node基础

### 配置环境变量
- node 可以在命令行下执行的原因：
	- 将可执行文件配置到了环境变量下

###node是什么
服务端运行js的环境，服务端语言

####前端的模块化
- 闭包 --- 一般都是闭包
- 单例模式 --- 不能完全解决命名冲突，调用时代码过长 
- requirejs (AMD) --- 依赖前置
- seajs (CMD) --- 就近依赖
- commonjs 规范 --- 是node模块的实现 ---  导出  module.exports 
####exports 和 module.exports 的区别：
1. module.exports 初始值为一个空对象 {}
2. exports 是指向的 module.exports 的引用
3. require() 返回的是 module.exports 而不是 exports
###node特点
#####I/O  input/output  输入/输出端口
- 异步 I/O --- 定时器、回调函数、事件...
- 单线程 (其他语言是多线程 )
- 进程：是包含线程的，node一个进程只能开一个线程（其他语言是一个进程可以开多个线程）

> 多线程的实现：就是切换执行上下文 --- 速度很快感觉不出来，好像在做很多件事

###事件环
- 靠事件驱动来实现的

###关于全局变量
- 前端的全局变量是window，服务端的是global
- 全局对象：在当前文件夹下可以直接使用的都是全局对象
- 全局对象global上的属性 
- 五个特殊的形参
- node中没有window属性，也不是global，是空对象{ }
- 同一个“作用域”下，变量不能声明两次  --- let / const ----- 作用域就是 `{ }`

```
// node中没有window属性
console.log(this);// 全局中的this是空对象 {} , 不是global

// 定时器中的this是定时器自己
setTimeout(function () {
    console.log(this);
});

// 闭包中的this才是global
~function () {
    console.log(this);// global
}();


// var 不能直接将内容挂载到global上
var a = 100;
console.log(global.a);// undefined
console.log(a);// 100
// 没有var声明的变量会自动挂载到global上
b = 200;
console.log(global.b);// 200
console.log(b);// 200

// 但是写代码不能丢掉var/let/const 以后需要变的用let  以后不需要变的用const
let c = 300;
const arr = []; // 只要内存地址不变时 可以改变内容

#### 箭头函数 es6

// 1.
function sum(a, b) {
    return a + b;
}

// let sum = (a,b) => {
//     return a+b;
// };

let sum = (a,b) => a+b;

// 2.
function d(a) {
    return function (b) {
        return a+b;
    };
}

// 如果用了 {}， 就一定要加return  只一个参数可以不用加()
let d = a => {
    return b => {
        return a + b;
    }
};

// let c = a => b => a+b;

// 调用
console.log(c(1)(2));
```
####global
1. console time  timeEnd  可以计算时间差
```
console.time('start')
for(let i=0;i<100;i++){}
console.timeEnd('start')
```
2. setTimeout

```
setTimeout(function(){
	console.loh(this);//this是定时器自己
},1000)

```
3. 改变函数中的this指向(call，apply)会导致函数执行 
    bind只能绑定一次
    var that=this   保存this指向
    使用箭头函数处理this  （箭头函数自身是没有this指向的  这一层里的this指向父级）
```
function a(){
console.log(this);
}
var fn=a.bind(1).bind(2)
fn(); //bind只能绑定一次
```