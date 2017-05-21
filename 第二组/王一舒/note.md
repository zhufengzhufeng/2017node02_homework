#NODE
###brew
https://brew.sh/index_zh-cn.html
brew install git
###告诉git你是谁
git config --list 查看配置
git config --global user.name 用户名 
git config --global user.email 邮箱
###创建目录
mkdir 目录名字
###cd 进入目录
cd 目录名
mkdir test-git && cd test-git
###初始化git仓库
git init （初始化）
ls -al 查看所有文件 包括隐藏文件
###创建文件
touch index.txt
###查看文件内容
cat index.txt
###vi常用命令
i  插入
esc+ :wq 保存并推出
###查看git状态
红色表示没有在暂存区中
绿色表示在暂存区中
git status
###加入暂存区
git add .
###加入历史区
git commit -m ''
###查看历史
git log --oneline
###git diff
git diff  比较工作区和暂存区
git diff --cached 暂存区和历史
git diff master 工作区和历史区
###从暂存区中覆盖掉工作区
git checkout 文件名
###选择某个版本进行回滚操作
git reset --hard 版本id
###查看所有历史版本
git reflog
###创建gitignore必须在add之前创建
.idea
node_modules
.DS_Store
###删除上一次添加暂存区的内容
git reset HEAD .
###分支
git branch (查看分支)
git branch 分支名 (建立分支)
###创建的分支和master一样
git branch -D 删除分支
###创建并切换
git checkout -b 分支名 
=>
git branch dev
git checkout dev
###将内容提交到某个分支上
默认我们的代码是放在工作区上，不属于任何分支，只有提交到某个分支上，此文件才归属于特定的分支
###fast-forward
主干没有任何更新
分支提交了新的代码
将主干的指针快速指向到分支最新的代码即可
###提交过的文件可以一步到位
git commit -a -m 'add hello'
###conflict
合并多个分支时可能合并的内容会产生冲突
手动解决冲突,提交最新结果
###创建有内容的文件
echo "# 201702nide" > README.md

##提交到远程仓库

###建立文件
README.md
.gitignore
###提交到历史区
git add
git commit -m ‘信息’
###查看远程仓库
git remote -v
git remote add 地址的别名 地址
git push origin master 将master推送到origin上
###本地和线上版本不一致
线上比线下的版本新
线上和线下两个版本都不一致
###拉取最代码
将线上最新代码拉取到master分支上
git pull origin master 获取最新代码
###部署git静态网页
- 将网页通过git网址访问（只能放静态页，不能放置server）
###第一步
- 需要一个特定的分支（gh-pages）
git checkout -b gh-pages
- 将代码提交到这个分支上
git add ```
git commit -m'static'
- 建立本地和远程的链接
git remote add 别名 地址
- 推送到github上,将gh-pages提交到这个分支上
git push origin gh-pages
- 在github中的setting上可以找到这个网址
###代码合并请求管理提交的笔记

###fork
叉子，将别人的代码当前的状态，克隆一份放到自己的仓库上，一个项目只能fork一次，我的代码更新不会导致你的项目更新
###clone
克隆是将线上的项目拉取到本地，拉下来后就是git仓库，而且已经添加好了远程仓库地址
git clone 地址 文件夹名字
###组长提交信息
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git push origin master
###组员给提交给自己
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git remote add leader 组长的地址（建立一次即可）
git pull leader master
git push origin master
###组长再次提交给老师
将自己的内容放进去
git add .
git commit -m 'team xxx'
git remote add teacher https://github.com/zhufengzhufeng/2017node02_homework
git pull teacher master
git push origin master

##NODE
###配置环境变量
- node可以在命令行下执行的原因
- 将可执行文件配置到了环境变量下
   - 系统->属性->高级系统设置->环境变量->path->新增即可
###node是什么？
服务端运行js的环境，服务端语言
###前端的模块化：
- 闭包
- 单例(有且只有一份): 不能完全解决命名冲突，调用时代码过长
- requirejs(AMD)依赖前置 seajs(CMD)就近依赖
commonjs 规范，是node模块的实现 module.exports
###node特点
- 异步io （定时器,回调函数）
- 单线程(其他语言多线程) 多线程实现就是切换执行上下文(速度很快感觉不出来，好像在干很多件事)
- 进程是包含线程的，node一个进程只能开一个线程
###事件环
- 靠事件驱动的
###全局对象
- 前端的全局变量 是window 服务端是global
- 全局对象，在当前文件夹下可以直接使用的都是全局对象
- 全局对象 global上的属性 + 五个特殊的形参
- node中没有window属性
```
setTimeout(function () {//定时器中的this 是定时器自己
    console.log(this);
});
~function () {
    console.log(this); //闭包中的this才是global
}();
```