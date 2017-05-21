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

定时器里的this 是自己 

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