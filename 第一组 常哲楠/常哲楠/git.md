#53正十4(git)

###集中式/分布式
>GIT是分布式版本控制系统
- 集中式：中央服务器。缺点：每个文件夹下都有叫`.svn`文件
- 分布式：每个人都有自己的完整项目代码，只是GIT是一个中转站。所有内容都存到`.git`下


GIT的优点：
- 开源
- 历史记录
- 团队协作
- 解决代码冲突，这个只是标明，还得手动解决

##使用GIT
1. 下载
2. 配置个人信息
```
//查看
git config --list

//配置全局的用户名和邮箱
git config --global user.name '一般和GITHUB名字相同'
git config --global user.email '377757708@qq.com'
```

3. 进入管理文件夹`cd 目录`
4. 初始化GIT仓库，一个仓库只能初始化一次，不要在其子文件夹再`git init`
5. 创建文件`touch`可以创建隐藏文件，还可以创建以`.`开头的文件
6. 查看文件内容`cat index.html`
7. 编辑文件`vi index.html`
	- 编辑模式`i`
	- 退出编辑`esc` 
	- 保存退出`:wq`
8. GIT的三个区：工作区-->暂存区/缓存区/过渡区-->历史区/版本库。这些都是本地操作
	- 工作区-->暂存区：`git add .`
	- 暂存区-->历史区：`git commit -m 'reason'`，必须填写提交信息
9. 查看git 状态：`git status`
	- 红色表示不在暂存区
	- 绿色表示在暂存区
10. `git log` `git log --oneline`，可以查看历史会生成一个版本号，还有提交信息


###对比代码
`git diff`
- 工作/暂存`git diff`
- 暂存/历史`git diff --cached`
- 工作/历史`git diff master`

###各种滚
####暂存区替换掉工作区
如果在工作区修改后
可以使用`git status`看一下
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

就会有提示
`git checkout -- <file>`


###历史覆盖工作区
因为历史区有很多版本号，所以可以根据版本号来回滚
```
//这个id至少7位，可以在git log --oneline里查看
git reset --hard id
```
如果回到之前的版本，那么最后提交到回到的那个版本的之间的版本就没有了
但是，可以通过`git reflog`查看所有历史版本


###GUI
界面化
- sourceTree
- webstrom

###忽略文件
创建根目录下的`.gitignore`
一般会忽略
```
.idea
node_modules

//MAC下的
.DS_Store
```

###误操作
提交到缓存区后，因为两次一样，不可以回滚
可以`git staus`查看一下命令

```
//删除上一次添加到暂存区的内容
git reset HEAD .
//再回滚就可以
git checkout .
```

###分支
查看分支
`git branch`
当前在哪个分支前面就有一个星号

加分支
`git branch 分支名`

创建的分支和master一样

切换分支
`git checkout 分支名`

删除分支
`git branch -D 分支名`
注意不可以在分支内删除分支

**创建并切换到分支**
`git checkout -b dev`

默认我们的代码是放到工作区上的，不属性于任何分支
将文件提交到某个分支上，才是那个分支


###合并分支
####fast-forward
主干没有任何更新
分支提交了新的代码
这是最快的方式

切到master
`git checkout master`
吞并
`git merge 分支`
如果分支没用，再手动删除分支

####conflict
只支持提交过的文件，可以将add 和 commit 合并写
`git commit -a -m 'message'`

合并多个分支时，合并的内容可能会产生冲突，手动解决冲突，提交最新结果


###提交远程
github展示的是历史区的内容，也就是commit的内容

创建有内容的文件
```
echo '内容' >> README.md
```

必要的文件
- README.md
- .gitignore


提交到历史区
第一次提交不可以使用
`git commit -a -m ''`

连接远程仓库
查看所有远程
`git remote -v`
第一次
origin 就代表url
使用https的url
```
git remote add origin url
```
然后
```
git push origin master
//将master推送到origin上
```

如果之前推送到master的时候，如果加了一个`git push origin master -u`，那么之后推送的时候，直接使用`git push`就可以推送到master上了

####线上线下不一致
第一种，线上自己改了，而线下也有改动的话，推送之前，要选拉取最新代码

拉取最新代码
```
//获取最新代码拉到master上
git pull origin master
```

###布属静态网页
网页通过(git)网址访问（只能放静态网页，而不能放server）
- 需要一个特定的分支`gh-pages`
- 将代码提交到这个分支上
- 再推送到github上，推送的是`gh-pages`分支
- 就可以在github的setting上找到这个网址

两个本地文件连接一个git仓库的话也可以直接提交，只要编辑的不是同一处文件




###作业
代码合并

fork将别人代码当前的状态克隆一份，放到自己的仓库上，一个项目只能fork一次，如果想fork多次，只能删除再次fork，我的代码更新不会导致你的项目

克隆，是将线上的项目拉取到本地，拉下来后，就是git仓库，而且已经添加好了远程仓库地址
不要去修改那些README.md或.gitingnore

去新建一个文件夹
在里面添加文件
再出来在根目录
```
git add .
git commit -m ''
git push origin master
```

发送合并请求，必须是fork的关系
pull request



如果是组员提交的话
```
git add .
git commit -m ''
//推送之前要先拉取一下
//要关联一下
git remote add 组长名字 地址
git pull 组长名字 master
//之前再推送
git push origin master
```

