##配置信息列表
`git config --list`
##配置用户
`git config --global user.name xxx`
`git config --global user.email xxx@xx`
## GIT bash 基础
`~/Desktop`  ~ 系统用户
`mkdir` 目录名字
`cd`  进入目录
`git init` 初始化 git 仓库
`master`  主分支
`ls -al` 查看所有文件（包括隐藏文件）
`toucn`  创建文件 （隐藏文件 以及 .gitginore）
`cat`   查看文件内容
`vi`   编辑文件
       进入后 默认编辑模式   `i - insert` 进入插入模式    保存退出  `esc`  `:wq`   




## CLI GUI 两种方式 
命令行  图形界面
## GIT 仓库
- 工作区       ：真实存放文件  
- 暂存区/缓存区/过渡区 
- 历史区/版本库   ：版本号

`git status` 查看git状态
- 红色 ： 没有在暂存区中
- 绿色 ： 在暂存区中

`git add .` / `git add a`  所有文件加入暂存区    ->暂存区

`git commit -m`   加入历史区  `-m` message      ->历史区 

`git log`  日志    `--oneline`  显示一行 
`commit 9f622acc99ebe6138ded59a1e9d392049da0c0c6`  : 版本号  (至少7位有效)

## 文件对比 工作区 暂存区 历史区
`git diff`  文件对比  默认 工作区 -- 暂存区
`git diff --cached`  暂存区 -- 历史区
`git diff master`    工作区 -- 历史区

## 文件回滚
- 暂存区 覆盖 工作区
`git checkout .`  放弃本次修改 暂存区 覆盖 工作区
- 历史区 拉回 工作区
`git reset --hard version`  选择某个版本进行回滚操作    硬回滚
`git reflog`   查看所有历史版本

`git reset HEAD . ` 回到上一次添加到暂存区的内容 （暂存区）
## 忽略文件
`.gitignore`   文件夹/文件名  `.idea  node-modules ` `DS_Store` mac
创建 .gitignore  必须在 add 之前


### source tree

## 分支管理
`git branch`  查看分支  `*` 分支位置
`git branch xxx`    建立分支          创建的分支和 master 一样
`git checkout xxx`  切换分支    
`git branch -D xxx`  删除分支   不能在分支上操作
`git checkout -b dev`  创建并切换    `git checkout dev` `git branch dev`
### 将内容提交到某个分支上
默认我们的代码是放在工作区上，不属于任何分支。只有提交到某个分支上 此文件才归属于特定的分支 : add commit
###合并分支
`git merge`  fastforward  主干没有任何更新，分支提交了新的代码 将主干的指针快速指向到分支最新的代码即可

`git commit -a -m 'message'` 提交过的文件可以一步到位提交   
###conflict
合并多个分支时会产生冲突
手动解决冲突，得到想要的结果


## github
展示的是 历史版本
## 本地有 远程空
`echo "content" > README.md`     > 到哪  >>追加  `echo` 输出
`git init`
`touch .gitignore`      : README.md  .gitignore  (必备)
`git add .`  
`git commit -m 'first commit'`


## 远程仓库
`git remote -v`  查看远程仓库
`git remote add origin url` 
`git push origin master`     方法 push  目标 origin 分支 master 

## 本地和线上版本不一致
- 线上比线下的版本新
- 线上 线下两个版本不一致

## 拉取最新代码
- 将线上最新代码拉取到 master 分支上
`git pull origin master`


## 部署 git 静态网页
- 将网页通过 git 网址访问（只能放静态页，不能防止 server）
### 第一步
- 需要一个特定的分支 （ gh-pages ）
- 将代码提交到这个分支上
  `git add .`
  `git commit -m 'static'`
  `git push origin gh-pages`
- 建立 本地和远程的连接
- 推送到 github 上 将gh-pages 提交到这个分支上

- 在 github 中的 setting 上可以找到这个网址
> 默认 index.html  当前目录作为根目录

## 代码合并请求管理提交的笔记
###fork 
- 叉子 将别人的代码当前的状态 克隆一份放到自己的仓库 
    一个项目只能 fork 一次
    我的代码更新不会导致你的项目更新
###clone
- `git clone  url filename[opt]`  克隆是将线上的项目拉取到本地。拉下来就是 git 仓库
                                    而且已经添加好了远程仓库地址
**空文件不会被提交**

### 组长提交信息

git remote add leader url
git pull leader master




