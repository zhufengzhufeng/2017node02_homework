[toc]
# Git 和 Node基础

## git命令

### 同步新仓库
`git clone https address`
### 查看仓库和远程仓库是否建立联系（进入仓库）
```
git remote -v
origin  https://github.com/realoneme/first.git (fetch)
origin  https://github.com/realoneme/first.git (push)
```
### 把本地文件同步到git上
```
git add ./-A(用.或者-A)
git commit -m "comments"
git push origin master //推送到主干
```
### git config(新用户设置用户名和email)
```
git config --global user.email"xx@xx.com"
git config --global user.name"Your Name"
```
### 拉取代码（在这个仓库下）
```
git pull origin master
```
### 通过fork别人的仓库，在本地修改别人的代码
```
git remote add newname 别人仓库地址
git remote update newname
git pull newname master
```
然后就可以得到别人的代码在自己的仓库里

### 添加git共同开发者权限
1. 添加协作人员
2. 进入 仓库 点击 settings -> collaborators 在里面 添加协作人员（git账户名）-> 点击Add collaborator
3. 协作人员 会收到 邮件 同意下 即可

注意：每个人员在 git push 之前 一定要 先 git pull 一下 然后再 git push


## 创建自己的git仓库

### 创建目录
```
mkdir folder-name
```
并且支持连写，创建并进入目录
```
mkdir folder-name && cd folder-name
```
### 初始化文件夹
```
git init
```
### 查看所有内容（以及隐藏文件）
```
ls -al
```
### 创建文件
```
touch index.txt (创建一般文件)
touch .index(可以创建以.开头的文件)
```
### 查看文件内容
```
cat index.txt
```
### 在文件中写内容
```
vi index.txt(进入编辑界面)
i 进入编辑模式
esc :q!(强制不保存退出)
esc :wq(保存并退出)
```
### 提交文件到暂存区
```
git add filename / git add . /git add -A
```
快速提交，只针对提交过的文件有效
```
git commit -a -m '注释'
```
### 提交文件到历史区
```
git commit -m'需要的提交注释'
```
如果没有`-m '注释'`,就需要在编辑状态加上注释，:wq保存退出
### 查看git状态
```
git status
```
- 红色表示没有在暂存区中
- 绿色表示在暂存区中

### 查看git历史
```
git log
commit b3d4f15034d58d2d805293bf4580fe2e8e88a956  （唯一版本号）
Author: Rebecca <mostsweethoney@qq.com>
Date:   Sat May 20 10:30:39 2017 +0800

    test
```
```
git log --oneline
b3d4f15 test

```
```
git reflog
查看所有历史版本
```

### 文件对比
```
git diff 比较工作区和暂存区
git diff --cached 比较暂存区和历史区
git diff master 比较工作区和历史区
```

### 从暂存区覆盖掉工作区
```
git checkout 文件名
```

### 从历史区覆盖掉工作区
```
git reset --hard id号
```

### 删除上一次添加暂存区的内容
1. 先从历史区覆盖暂存区
2. 再从暂存区覆盖工作区
```
git reset HEAD 文件名/git reset HEAD .
```

```
git checkout 文件名
```

## 界面化工具
### sorceTree
### webstorm插件
在提交之前创建.gitignore文件

## 分支管理
### 查看分支
```
$ git branch
* master(现在在master)
```
### 建立分支
先要在主干上提交过，才可以建立分支
```
git branch 分支名
```
**创建的分支和master一样**
### 切换分支
```
git checkout 分支名
```
### 删除分支
```
git branch -D 分支名
```
### 创建并切换到分支
== git branch 分支名 + git checkout 分支名
```
git checkout -b dev
```
### 将内容提交到某个分支上
（默认将代码放在工作区上，不属于任何分支，只有提交到某个分支上的时候，此文件才归属于特定的分支）
#### fastForward
主干没有任何东西，分支提交了新的代码，就可以将主干的指针快速指向到分支最新的代码上
```
git merge 分支名
```
合并之后将分支删除，本次合并结束
#### 手动解决冲突
当master和分支有冲突的时候，要手动改文件解决冲突，再在master上提交代码

# 远程操作
## 建立文件
- README.md
- .gitignore

## 提交到历史区
- git add
- git commit -m

## 查看远程仓库
git remote -v

## 建立远程仓库
git remote add origin (git 地址，用https的)

## 把代码推到线上
git push origin master -u (设置默认推送位置，以后只要写git push)

### github发布页面（只能访问静态页，不可以防止server）
- 需要一个特定的分支 gh-pages
- 将代码提交到这个分支上
- 推送大github上
- 在github的setting中可以找到这个网站

进入到自己项目目录 打开命令行窗口 git init 将项目目录 初始化为本地仓库
然后 本地仓库和自己新建远程仓库 建立 联系
- git remote add origin https://github.com/liwenli111/webApp.git
- git add .
- git commit -m"update"
- git push origin gh-pages
- 进入Settings 在下面会看到一个链接 （网页名称）
https://liwenli111.github.io/webApp/index.html

## fork
将别人代码的当前状态clone一份放在自己的仓库里，一个项目只能fork一次。原代码更新不会导致fork的代码更新
## clone
将线上的项目拉取到本地，拉下来之后就是git仓库并且已经添加好了git地址
```
git clone url 别名  (来克隆项目，并起别名)
```
```
pull request 是向fork来的项目人发起合并请求
```
git remote add leader leader的地址
$ git pull leader master（pull别人的仓库地址）
合作开发提交代码的时候，需要先拉取代码，再push上去

## node基础知识
### node可以在命令行下执行的原因：
将可执行文件配置到了环境变量下

### node是服务端运行js的环境
可以让js跑在服务端里，操作文件系统，模块，包，操作系统API
### 前端模块化
- 闭包
- 单例模式（不能解决命名冲突，调用时代码过长）
- requirejs(AMD)依赖前置  seajs(CMD)就近依赖，需要的时候再引进来这个模块
- commonjs规范，node模块的实现
### node特点
- 异步IO（定时器，回调函数）
- 单线程
（多线程实现：切换执行上下文，因为执行速度很快，所以感觉再做很多件事情）
- 进程（包含线程），node一个进程只能开一个线程
### 事件环
- 靠事件驱动（当前的事件和之后的事件）

### 全局对象
前端的全局变量是window，服务端的是全局对象，是global
在当前文件夹下可以直接使用的，都是全局对象
例如：`console`
#### 全局对象的组成
global上的属性，和五个特殊的形参。
**node中没有window属性**
node中的this是{}。
- var 不能直接将内容挂载在global上，
- 没有var声明的，会挂载在global上。

> 同一个“作用域` { }`”下 变量不能声明两次，如果使用了`{ }`，必须要写return


```
/*function a(a) {
    return function (b) {
        return a+b;
    }
}*/
let sum  = a => b=> a+b;(ES6箭头函数)
```