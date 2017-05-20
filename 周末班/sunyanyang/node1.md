# JS B Git

标签（空格分隔）： Git

---

[toc]

## git命令
### 同步新仓库
`git clone https address`
### 查看仓库和远程仓库是否建立联系（要进入仓库）
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