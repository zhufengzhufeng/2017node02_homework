#git配置
- git config --list
- git config --global user.name 密码
- git config --global user.email 
#git分区
  1. 工作区
  2. 暂存区/缓存区/过渡区
  3. 历史区/版本库
#查看git状态
- git status:
- 红色表示没有在暂存区中
- 绿色表示在暂存区中
#CLI(命令行模式) GUI(界面模式)
#查看历史
- git log 
#不同点
- git diff:比较的是工作区和暂存区
- git diff --cached:比较历史区和暂存区
- git diff master:比较历史区和工作区
#从暂存区中覆盖掉工作区
- git checkout 文件名
#从历史区覆盖掉工作区
- git reset --hard id
#回到上一版本
- git reset --hard 版本id
#查看所有历史版本
- git reflog
#创建gitignore必须在add之前创建
- .idea
- node_modules
- .DS_Store
#删除上一次添加暂存区的内容
- git reset HEAD .
#将内容提交到某个分支上
- 默认我们打代码时放在工作区上,不属于任何分支,只有提交到某个分支上,此文件才归属于特定的分支
#fast-forward
- 主干没有任何更新
- 分支提交了新的代码
- 将主干的指针快速指向到分支最新的代码即可
#提交过的文件可以一步到位
- git commit -a -m""
#confilct
- 合并多个分支时可能合并的内容会产生冲突
- 手动解决冲突,提交最新结果
```
  git checkout master //切换到master分支上
  git branch -D dev   //删除dev分支
  git branch          //查看分支
  git checkout -b dev  //创建并切换到新分支dev上
  touch index.js       //创建文件
  git status           //查看git状态
  git add .            //加入暂存区
  git commit -m 'add index'  //加入历史区
  git merge dev          //合并
  git log              //查看历史
  vi index.js         //编辑文件
  git reset HEAD .  //删除上一次添加暂存区的内容
  git commit -a -m 'write Hello'
  cat index.js       //查看文件
```
#iterm2插件/oh my zsh for mac
#提交到远程仓库
- README.md
- touch .gitignore
- git add 文件名
- git commit -m"描述"
- git remote -v 查看远程仓库
- git remote add 仓库名 仓库地址
- git push origin master
#本地和线上版本不一致
- 线上比线下的版本新
- 线上和线下两个版本都不一致
#拉取最新代码
- 将线上最新代码拉取到master分支上
- git pull origin master 获取最新代码 update
部署git静态网页
- 将网页通过git网址访问(只能放静态页,不能放置server)
- 第一步:需要一个特定的分支(gh-pages)---- git checkout -b gh-pages
- 第二步:将代码提交到这个分支上  git add .       git commit -m''''     
- 第三步:建立本地和远程的连接 git remote add  别名(origin) 地址
- 第四步:推送到github上 ,将gh-pages提交到这个分支上 git push  origin gh-pages
- 第五步:在github中的setting上可以找到这个网址
#代码合并 
##组长提交信息
- git clone 自己的库地址(从老师库fork过来的)
- git add .
- git commit -m""
- git push origin master
##组员提交信息
- git clone 自己的项目地址
- git add .
- git commit -m "xxx 的homework"
- git remote add leader 组长的地址(建立一次即可)
- git pull leader master
- git push origin master
- new pull request
#Node
##配置环境变量
- 系统->属性->高级系统设置->环境变量->path->新增
#node定义
- 服务端运行js的环境，服务端语言

##前端的模块化：
- 闭包
- 单例(有且只有一份): 不能完全解决命名冲突，调用时代码过长
requirejs(AMD)依赖前置 seajs(CMD)就近依赖
commonjs 规范，是node模块的实现 module.exports
##node特点
- 异步io （定时器,回调函数,事件,ajax）
- 单线程(其他语言多线程) 多线程实现就是切换执行上下文,
进程是包含线程的，node一个进程只能开一个线程
#全局变量
- 前端的全局变量是window 
- 服务端是global
- 全局对象在当前文件夹下可以直接使用的都是全局对象
- 全局对象 global上的属性 + 五个特殊形参
- node中没有window 属性
- node中的this是{},不是global
