# node（二期）
## webstorm破解码
http://idea.iteblog.com/key.php
# git
#### 小百科
- git是一款免费、开源的分布式版本控制系统，用于敏捷搞笑的处理任何或大或小的项目。
#### Git的功能特性：
##### 1、从一般开发者的角度看git有以下功能：
> 1、从服务器上克隆数据库
> 2、在自己的机器中创建分支，修改代码
>3、在单机上自己创建的分支上提交代码
>4、在单机上合并分支
>5、新建一个分支，把服务器上最新版的代码fetch下来，然后跟自己的主分支合并。
>6、生成补丁（patch），把补丁发送给主开发者。
>7、看主开发者的反馈，如果主开发者发现两个一般开发者之间有冲突（他们之间可以合作解决的冲突），就会要求他们先解决冲突，然后再由其中一个人提交。如果主开发者可以自己解决，或者没有冲突，就通过。
>8、一般开发者之间解决冲突的方法，开发者之间可以使用pull 命令解决冲突，解决完冲突之后再向主开发者提交补丁。



### 用户设置
- 安装完成之后，还需要在命令行输入设置：

#### 告诉git你是谁
```
git config --list 查看配置
git config --global user.name "wangwei2017_1"
git config --global user.email "1129942397@qq.com"
```
>-  Git是分布式版本控制系统，所以每个机器都必须填写自己的名字和Email地址。
>-  注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

### 创建目录及文件或删除文件

#### 创建目录
```
mkdir 目录名字
```
#### cd 进入目录 
```
cd 目录名
mkdir test-git && cd test-git
pwd   //显示当前环境的位置
```

#### 初始化git仓库
```
git init   （初始化）
ls -al    查看所有文件 包括隐藏文件
```

#### 创建文件
```
touch index.txt
```

#### 查看文件内容
```
cat index.txt
```

#### vi常用命令
- 在文件中插入内容
```
vi 文件名
i  插入
esc+ :wq 保存并推出
```
- 在文件中写入内容
```
echo 1 > index.txt
echo 2 >> index.txt
```
> - 把1输出到新创建的index.txt文件中     (  > 表示清空并写入)
> - 把2追加到index.txt中 （ >> 表示在原来文件的末尾追加）
#### 删除文件
```
rm index.txt
```

### 文件添加到暂存区并推送到历史区
#### 查看git状态
```
git status
```
> - 红色表示没有在暂存区中
> - 绿色表示在暂存区中

#### 加入暂存区
```
git add index.txt //只添加index.txt
git add .   //整体推送
```
#### 加入历史区
```
git commit -m'注释'
```
>- 如果你没有添加-m后面参数的话表示会弹出一个编辑页面，可以输入你的注释然后按esc退出编辑模式，再输入:wq!退出此编辑器。 
>- git commit命令执行成功后会告诉你，1个文件被改动（index.html文件），插入了两行内容（index.html有两行内容）。
>- 为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：

### 代码对比和回滚问题

#### 查看历史（版本）
```
git log --oneline
```




#### git diff
```
git diff  比较工作区和暂存区
git diff --cached 暂存区和历史
git diff master 工作区和历史区
```

#### 从暂存区中覆盖掉工作区
```
git checkout 文件名
```

#### 选择某个版本进行回滚操作
```
git reset --hard 版本id
```

#### 查看所有历史版本
```
git reflog
```
#### 创建gitignore必须在add之前创建
```
.idea
node_modules
.DS_Store
```

#### 删除上一次添加暂存区的内容
```
git reset HEAD .
```

---------------------------------------------------------------------------
---------------------------------------------------------------------------




## 分支问题 
```
git branch (查看分支)
git branch 分支名 (建立分支)
创建的分支和master一样
git branch -D 删除分支
```

#### 创建并切换
```
git checkout -b 分支名(dev) 
=>
git branch dev
git checkout dev
```

#### 合并分支
```
git merge 分支名
```
> 默认master是主干，用主干和并分支
> 合并分支后 被合并的分支需要删除
> 合并完成之后，将合并后的文件再次上传
#### 删除分支
```
git branch -D dev
```

#### 将内容提交到某个分支上
默认我们的代码是放在工作区上，不属于任何分支，只有提交到某个分支上，此文件才归属于特定的分支

## fast-forward
- 主干没有任何更新
- 分支提交了新的代码

> 将主干的指针快速指向到分支最新的代码即可

#### 提交过的文件可以一步到位
```
git commit -a -m 'add hello'
```

#### conflict（处理冲突）
- 合并多个分支时可能合并的内容会产生冲突
- 手动解决冲突,提交最新结果


#### oh my zsh
http://ohmyz.sh/

#### item2
http://www.iterm2.com/documentation.html

#### 创建有内容的文件
```
echo "# 201702nide" > README.md
```


-------------------------------
-------------------------------

##二、 Git-remote提交到远程仓库
#### 建立文件
- README.md
- .gitignore
- 要忽略的文件需要在.gitignore建立之后再add.
> git不能提交空文件夹


#### 提交到历史区
- git add
- git commit -m '信息'

#### 查看远程仓库
```
git remote -v
```
#### 关联仓库
```
git remote add 地址的别名 地址
git push origin master 将master推送到origin上
```

#### 本地和线上版本不一致
- 线上比线下的版本新
- 线上和线下两个版本都不一致


#### 拉取最代码
- 将线上最新代码拉取到master分支上
```
git pull origin master 获取最新代码
```

## 部署git静态网页
- 将网页通过git网址访问（只能放静态页，不能放置server）
- 必须当前项目下建立一个`gh-pages`的分支
- 将我们需要发布的内容推送到`gh-pages`这个分支上
- `gh-pages`是固定值
- 推送到远程仓库上即可
- github会给你一个在线地址
#### 第一步
- 需要一个特定的分支（gh-pages）
```
git checkout -b gh-pages
```
- 将代码提交到这个分支上
```
touch index.js
git add ```
git commit -m'static'
```
- 建立本地和远程的链接
```
git remote add 名 地址
```
- 推送到github上,将gh-pages提交到这个分支上
```
git push origin gh-pages -u
```
- 在github中的setting上可以找到这个网址


------------------------------------------------------------
------------------------------------------------------------

##三、 代码合并请求管理提交的笔记

#### fork
- 叉子，将别人的代码当前的状态，克隆一份放到自己的仓库上，一个项目只能fork一次，我的代码更新不会导致你的项目更新

#### clone
- 克隆是将线上的项目拉取到本地，拉下来后就是git仓库，而且已经添加好了远程仓库地址
```
git clone 地址 文件夹名字
```

#### 组长提交信息
```
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git push origin master
```

#### 组员给提交给自己
```
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git remote add leader 组长的地址（建立一次即可）
git pull leader master
git push origin master
```

#### 组长再次提交给老师
```
将自己的内容放进去
git add .
git commit -m 'team xxx'
git remote add teacher https://github.com/zhufengzhufeng/2017node02_homework
git pull teacher master
git push origin master
```

> 每个人提交今天的内容
