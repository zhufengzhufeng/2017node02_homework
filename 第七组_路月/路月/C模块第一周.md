#C模块第一周
[TOC]
##git
>-svn存储文件每一个文件下都有.svnde 的文件；git 所有内容都存到.git

```
// 查看配置
git config --list
// 配置
git config --global user.name meluyue
git config --global user.email meluyuey@gmail.com
```
###常用命令
>- mkdir 目录名字
```
mkdir test
```
>- cd 进入目录
```
mkdir test（tab补全）
```
>- git init  初始化git仓库
>- ls      ls -al  查看文件夹目录
>- touch 创建文件
```
touch index.txt
```
>- cat 查看文件内容
```
cat index.txt
```
>- vi 编辑文件
```
i/a>esc>:wq保存并退出/q!强制退出>回车
```
###git 提交
>- git status  查看所有状态
	- 红色表示没有在暂存区中
	- 绿色表示在暂存区中
> 加入到暂存区
```
git add .  (. -A 所有文件)
```
> 加入到历史区	
```
git commmit -m'备注信息'
```
>- git log  查看日志
>git log --oneline
>- git diff 查看不同  
	- git diff 工作区和缓存区
	- git diff --cached  暂存区和历史区
	- git diff master 工作区和历史区
###git回滚
>- git checkout 文件名  (从暂存区覆盖掉工作区)
>- git reset --hard 版本号最少七位 (从历史区覆盖掉工作区，需要指定某个历史区)
>- git reset HEAD 文件名  删除上一期暂存区提交的内容
###界面化工具
####sourceTree
####webstrom
创建 .gitignore 文件
编辑内容
 .idea 
node_modules popup
.DS_Store
VCS->配置VCS Operations popup
右击文件-->git-->add
右击文件-->git-->Commit file
###分支管理
####创建并切换
>- git branch 查看分支
>- git branch 分支名   建立分支（创建的分支和master一样）
>- git checkout 分支名  切换分支
>- git branch -D 分支名  删除分支
>- git checkout -b 分支名 创建并且换
####将内容提交到某个分支上
默认我们的代码是放在工作区上，不属于任何一个人分支
把新建的文件放到xx分支上
git add .
git commit -m '备注'	 
git commit -a -m '备注'   只支持提交过的文件  一步到位 
####分支合并
>- git merge 分支名
	- fast-forward 主干没有任何更新，分支提交了代码，将主干的指针快速指向到最新的代码 
	- conflict 合并多个分支是可能存在冲突，如果有冲突 手动解决再提交

###远程连接
####创建有内容的文件
```
echo "# node_homework" >> README.md  //node_homework 仓库名  >> 追加
```
把文件推送到GitHub上
- 1 新建一个空文件
- 2 github新建一个仓库
- 3 `$ echo "# node_homework" >README.md` node_homework仓库名，新建README.md文件写入内容
- 4 git init 初始化git
- 5 touch .gitignore  新建.gitignore文件
- 6 vi .gitignore文件写入内容 
 .idea
node_modules
DS_Store
- 7 git add .
-  8 git commit -m 'xx'
-  9 git remote add origin https://github.com/meluyue/node_homework.git
- 10 git push origin master
origin  是远程的别名    master分支
####拉去最新代码
- git pull origin master
- git push origin master
####部署git静态网页
- 1 将网页通过git网页地址访问（只能是静态网页，不能放置server）
- 2 要求
	- 需要一个特定的分支 gh-pages
	- 将代码提交到这个分支上
	- 推送到github上
	- 在github上可以找到这个网址（Branch-->gh-pages-->settings-->github pages地址访问）
```
git checkout -b gh-pages
// 在这里新建文件准备推进
git add .
git commit -m'index' // 不能用连写，之前没有该文件
git push origin gh-pages
```
- git romote -v 查看远程连接
###代码合并请求
####组长提交给老师
- fork将别人的代码的当前状态，克隆一份到自己的仓库，一个仓库只能fork一次
- clone 将线上的项目拉去到本地，拉下来后就是git仓库，而且添加好了远程仓库
git clone 地址 文件夹名字（起新名字）
- 新建信息文件
- git add .
- git commit -m'XX'
- git push origin master
- github中点击new pull request点击绿色添加

再次提交
- git add .
- git commit -m'XX'
- git remote add teacher 自己地址 （建立一次即可，leader别名）
- git pull teacher master  （提交之前先拉取最新的代码）
- git push origin master
- pull request github中点击new pull request点击绿色添加


####组员提交给自己
- fork将别人的代码的当前状态，克隆一份到自己的仓库，一个仓库只能fork一次
- clone 将线上的项目拉去到本地，拉下来后就是git仓库，而且添加好了远程仓库
git clone 地址 文件夹名字（起新名字）
- 新建信息文件
- git add .
- git commit -m'XX'
- git remote add leader 自己地址 （建立一次即可，leader别名）
- git pull leader master  （提交之前先拉取最新的代码）
- git push leader master
- pull request github中点击new pull request点击绿色添加

##node
###配置环境变量
- node可以在命令行下执行的原因，将可执行文件配置到环境变量下
###node是什么
服务端运行js的环境，服务器语言

前端模块化
- 闭包
- 单利 缺点：不能完全解决命名冲突；调用时代码过长

requirejs（AMD）依赖前置     seajs（CMD）就近依赖
commonjs 规范，是node模块实现
###node特点
- 异步I/O  （定时器、回调函数）
- 单线程  多线程实现切换执行上下文（速度很快，感觉不出来，好像同时在做多件事）
- 进程是包含线程，node一个进程只能开一个线程
###如何解决异步问题
使用回调函数
###事件循环
靠事件驱动的
###全局对象
在当前文件夹下可以直接使用的都是全局对象
- global上的属性+五个特殊的形参
- 服务端的this是{}
- 闭包里面的this是global
- 箭头函数中的this是它的上一层
- 定时器中的this是定时器中的自己
- var  不能直接将内容挂载到global上；没有var声明的会挂载到global上面，同一个作用域{}下一个变量不能声明多次 const let 不能同一个名字
```
const arr=[];
arr.push(100);
console.log(arr);  // [100]
```
箭头函数
```
function sum(a,b){
return a+b;
}
// 如果使用大括号，需要return
let sum=(a,b)=>{
return a+b;
}

let sum=(a,b)=>a+b;



function a(a){
    return function (b) {
        return a+b;
    }
}
let a=a=>b=>a+b;
```