## 部署git静态网页
> 将网页通过git网址访问（只能放静态页   ，不能放置server）

[toc]

- 需要一个特性的分支(gh-pages)
```
git checkout -b gh-pages
```
- 将代码提交到这个分支上
```
git add ...
git commit -m ''
```
- 建立本地和远程仓库的链接
```
git remote add 别名 地址
```
- 推送到github上，将gh-pages提交到这个分支上
```
git push origin gh-pages
```
- 在github中的setting上可以找到这个网址

## 代码合并请求管理提交的笔记 
### fork
叉子，将别人的代码当前的状态，克隆一份放到自己的仓库上，一个项目只能fork一次，我的代码更新不会导致你的项目更新 
### clone
克隆是将线上的项目拉取到本地，拉下来后就是git仓库，而且已经添加好了远程仓库地址 
```
git clone 地址 文件夹名字

```
### 组长提交信息 
```
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git push origin master

```
### 组员给自己提交
```
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git remote add leader 组长的地址（建立一次即可）
git pull leader master
git push origin master

```
### 组长再次给老师提交
```
将自己的内容放进去
git add .
git commit -m 'team xxx'
git remote add teacher https://github.com/zhufengzhufeng/2017node02_homework
git pull teacher master
git push origin master
 
```

 
