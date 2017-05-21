#git

##配置git用户和邮箱
```
git config --global user.name "用户名"
git config --global user.email "邮箱"
```

##查看所有配置

```git config --list
```

##初始化git
```
git init
```

##git中的三个区

工作区

暂存区

历史区

通过git add 添加到暂存区
```
git add '文件名'
```

##通过git commit 添加到历史区
```
git commit -m"注释内容"
```



##查看历史状态
```git log```



##不同区的代码比较
```
//工作区和暂存区
git diff

//暂存区和历史区
git diff --cached（--staged）

//工作区和版本库
git diff master
```
##撤销

撤销回git add的内容
git reset Head "文件名"
撤回文件
先从缓存区撤销,缓存区无内容，从历史区域撤销
git checkout "文件名"
有的时候我们希望提交时合并到上一次的提交 git commit --amend

##删除

删除暂存区和工作区
删除暂存区中的内容,并且保证工作区中的内容已经不存在


git rm "文件名"
若本地文件存在则不能删除，需要通过-f参数删除

仅删除缓存区
git rm --cached "文件名"


##恢复

恢复某个版本文件
git checkout commit_id filename 某个文件
通过版本id恢复
git reset --hard commit_id
恢复未来
查看当时回滚时的版本

git reflog
快速版本回退
git reset --hard HEAD^
$ git reset --hard HEAD~3
同步远程仓库

##添加远程仓库
git remote add origin "地址"

##添加忽略文件
touch .gitignore
echo .DS_Store
echo node_modules
echo .idea

##推送代码
git push origin master

##查看
git remote 查看名字
git remote -v 查看地址

##代码的合并
git fetch
git fetch

##拉取过来手动合并
git diff master origin/master
git merge origin/master
git pull

##拉取并合并
git pull

##分支
git branch
git branch 创建分支
git checkout a
git checkout -b c切换分支

##在master  git merge
git checkout b
git branch --merged 合并了哪些分支
git branch --no-merged 合并了哪些分支
git branch -d a 删除分支
git branch -D a 删除分支
