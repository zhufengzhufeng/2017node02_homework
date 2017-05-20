###git
####git 命令
`git config --lis`t查看配置
`git config --global user.name`用户名
`git config --global user.email`邮箱

`mkdir 目录名字`创建目录
`cd 目录名`进入目录
`mkdir test-git && cd test-git`创建test-git目录，并且进入

`git init`初始化
`ls -al`查看所有文件 包括隐藏文件
`touch index.txt`创建文件 包括不能创建的

`cat index.txt`查看文件的内容
`git status`查看git状态 红色表示没有在暂存区，绿色表示在暂存区

`git add .`加入暂存区
`git commit -m'描述'' `加入历史区
`git log --oneline`查看历史

`git diff`比较工作区和暂存区
`git diff --cached` 比较暂存区和历史区
`git diff master`比较公正区和历史区

`git checkout 文件名` 从暂存区覆盖掉公正区
`git reset --hard 版本id`选择某个版本进行回滚操作
`git reflog` 查看所有历史版本
`git reset HEAD`删除上一次添加暂存区的内容

`git branch`查看分支
`git branch 分支名`建立分支
创建的分支和master一样
`git checkout -b 分支名`创建并切换
`echo "# 201702nide" > README.md`创建有文件的内容


### #将内容提交到某个分支上
默认我们的代码是放在工作区上的，不属于任何分支，只有提交到某个分支上，此文件才归特定的分支

####提交过的文件可以一步到位
`git commit -a -m 'add hello'`

####conflict
- 合并多个分支是可能合并的内容会产生冲突
- 手动解决冲突，提交最新结果


###fork
- 叉子，将别人的代码当前的状态，克隆一份放到自己的仓库上，一个项目只能fork一次，我的代码代码更新不会导致你的代码更新

###clone
- 克隆是将线上的代码拉取代本地，拉下来就是git仓库，而且已经添加考虑远程仓库地址



##node
###node是什么
服务端运行js的环境，服务端语言

###前端的模块化
- 闭包
- 单例模式（有且只有一份）：不能完全解决命名冲突，调用时代码过长
- erquirejs(AMD)依赖前置  seajs(CMD)就进依赖
- commonjs 规范，是node模块的实现 module.exports

###node特点
- 异步 io (定时器，回调函数)
- 单线程 （其他语言多线程）多线程就是切换执行上下文（速度很快感觉不出来，好像在干很多事情）
- 进程是包含线程的，node一个进程只能开一个线程

###global
- 前端的全局变量是window 服务端是global
- 全局对象 ：在当前文件夹下可以直接使用的都是全局对象
- node 中没有window属性
- 定时器中的this是定时器
- 闭包中的this是global
- var 一个变量 不能直接将内容挂载在global上
- es6中函数简写，可以省略大括号和return，function.

###事件环
- 靠事件驱动的



