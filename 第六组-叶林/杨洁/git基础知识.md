## git基础知识
 [toc]
### 告诉git你是谁
```
git config --list 查看配置
git config --global user.name 用户名 
git config --global user.email 邮箱

```
### 创建目录
```
mkdir 创建目录名字
```
### 进入目录
```
cd 目录名
mkdir test-git && cd test-git
 
```
### 初始化git仓库
```
git init （初始化）
ls -al 查看所有文件 包括隐藏文件

```
### 创建文件
```
touch index.txt
```
### 创建有内容的文件
```
echo "# 201702nide" > README.md
```
### 查看文件内容
```
cat index.txt
```
### vi常用指令
```
vi  进入编辑页面
i   插入
esc+ :wq  保存并退出
esc+ :q!  强制退出
```
### 查看git状态
- 红色表示没有在暂存区
- 绿色表示在暂存区
```
git status
```
### 加入暂存区
```
git add A || git add .
```
### 加入历史区
```
git commit -m ''
```
### 查看历史区
```
git log --oneline
```
### git diff
- git diff比较工作区和暂存区
- git diff --cached暂存区和历史区
- git diff master 工作区和历史区

#### 从暂存区中覆盖掉工作区的
```
git checkout 文件名
```
#### 选择某个版本进行回滚操作
```
git reset --hard 版本ID
```
### 查看所有历史
```
git reflog

```
### 创建gitignore必须在add之前创建 
```
.idea
node_modules
.DS_Store
```
### 删除上一次添加暂存区内容
```
git reset HEAD
```
### 分支
```
git branch (查看分支)
git branch 分支名 (建立分支)
创建的分支和master一样
git branch -D 删除分支
```
#### 创建并切换
```
git checkout -b 分支名 
=>
git branch dev
git checkout dev
```
## 将内容提交到某分支上
默认我们的代码是放在工作区上，不属于任何分支，只有提交到某个分支上，此文件才归属于特定的分支 
### fast-forward 
- 主干没有任何更新
- 分支提交了新代码
> 将主干指针快速指向到分支最新的代码即可
#### 提交过的代码可以一步到位
```
git commit -a -m 'add hello'
```
### conflict 
- 合并多个分支时可能合并的内容会产生冲突
- 手动解决冲突，提交最新结果

## 提交到远程仓库
### 建立文件
```
 README.md
.gitignore
```
### 提交到历史区
```
git add
git commit -m ''
```
### 查看远程仓库
```
git remote -v
git remote add 地址的别名 地址
git push origin master 将master推送到origin上
```
### 本地和线上版本不一样
- 线上比线下版本新
- 线上和线下两个版本都不一样

#### 拉取最新代码
```
git pull origin master
```
