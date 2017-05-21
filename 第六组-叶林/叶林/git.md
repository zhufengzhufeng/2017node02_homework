#git
##界面化
>sourceTree
##初始配置
>`git config --list` 查看配置
>`git config --global user.name`用户名
>`git config --global user.email`邮箱
>`~/Desktop`   ~代表当前系统的路径
## webstorm破解码
>http://idea.iteblog.com/key.php
##英语
》discard放弃
###初始化
>`mkdir 目录名字`
>`cd 目录名字`
>`touch 文件名字`
>`cat 文件名字` 查看文件内容
>`mkdir test-git && cd test-git`
>ls -al查看所有文件，包含隐藏文件
>window默认不支持创建点开头的文件
##
###查看状态
>`git status`
>红色表示没有在暂存区中
>绿色表示已经在暂存区
###查看历史记录
>`git log` 显示提交的历史记录
>`git log --oneline` 显示简短的历史记录
>`git reflog` 查看所有历史版本
###查看不同
>`git diff`  工作区和暂存区比
>`git diff --cached` 暂存区和历史区
>`git diff master` 工作区和历史区
###版本回滚
>`git checkout 文件名` ，从暂存区将工作区覆盖掉
>`git reset HEAD 文件名或者点` 删除本次暂存区的提交
>`git reset --hard 版本号id`，选择某个版本进行回滚操作
##分支
>`git branch` 查看当前分支,和所有分支
>`git branch 分支名字` 建立分支 ，刚创建出来和master一样
>`git checkout 分支名字`切换分支
>`git branch -D 分支`删除分支 不能在本分支删除自己
>`git checkout -b 分支名字`创建并切换
>`git merge 分支名字`主分支合并副分支  快速前进 快速合并
###创建gitignore必须在add之前创建
>`.idea`
>`node_modules`
###将内容提交到某个分支
>默认我们的代码是放在工作区的，不属于任何分支，只有提交到某个分支上，此文件才归属于特定的分支
###fast-forward
>主干没有任何更新
>分支提交了新的代码
>将主干的指针快速指向到分支最新的代码即可
###conflict
>合并多个分支可能合并的内容会产生冲突
>手动金额就冲突 提交最新的结果
##提交到远程仓库
###建立文件
>README.md
>.gitigmore
###查看远程仓库
>`git remote -v`查看关联的所有的仓库
>`git remote add 仓库地址的别名 仓库的地址`
>`git push origin master` 将master推送到origin上
###部署静态网页
>只能通过git地址访问，只能放静态文件
>1.需要一个特定的分支（gh-pages）
>2.将代码推送到这个分支上
>在github该项目的setting上可以找到访问的网址
###本地和线上版本不一致
>线上比线下版本新 `git pull 仓库别名 仓库地址分支`
##代码合并请求管理提交的笔记
>`fork` 将别人的代码当前的状态，克隆一份放到自己的仓库上，一个项目只能fork一次，代码更新不会导致我的fork的代码更新
>`clone` 克隆是将线上的项目拉取到本地，拉下来就是git仓库，而且已经添加好了远程仓库的地址   `git clone 地址 自己的文件夹名字`
##组长提交信息
>1.`git clone 自己fork的项目地址`
>2.`添加内容 dit add .  git commit -m "日志 git push origin master"`
##组长再次提交给老师
>将自己的内容放进去
>`git remote add teaher 地址`
>`git pull teacher master`
>`git push origin master`
##new pull request