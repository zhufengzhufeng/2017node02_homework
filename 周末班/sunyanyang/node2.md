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