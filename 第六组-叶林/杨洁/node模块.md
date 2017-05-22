## node中的模块
node基于commonjs规范的，分为内置模块，自定义模块和第三方模块
[toc]
### 如何使用require使用模块
- 文件模块 引用是需要相对路径引用 ./ ../
- 第三方模块  写模块名字即可 不需要./ ../
- 内置模块直接引用
- 第三方模块+ -g只能在命令行下使用
### nrm模块
- nrm模块 默认下载模块通过的是npm下载，切换到国内 cnpm taobao
- (sudo) npm install nrm -g 安装后就会拥有全局命令nrm
- nrm ls 列出所有可用源 nrm test 测试源的网速
- nrm use 用哪个源

### 如何导出模块
- exports
```
1.如果使用exports导出必须通过属性添加，否则无法挂载在module.exports上
2.因为返回的是module.exports，所以可以直接改变module.exports的指针
```
- module.exports

### HTTP-server
- 帮用户启动一个服务，返回静态文件
```
npm install http-server -g

```
- 在想要问的文件夹下启动服务
```
http-server -p 4000

```
### nodeppt
- 安装nodeppt
```
npm install nodeppt -g
```
- 在想要执行的文件夹下,文件中包含slide 
```
nodeppt start
```
### 发布包
- 包必须要存在package.json文件 
```
npm init -y
```
- 切换到npm上
```
nrm use npm
```
- 登录、注册 
```
npm addUser

```
- 发布包
```
npm publish
```
### 查看占用端口
```
netstate -anto | findstr "8080"
ps -ef | grep node 
kill pid

```
### 搭建静态博客
- 安装hexo模块
```
npm install hexo-cli -g
```
- 生成博客项目
```
hexo init blog
```
- 进入目录安装依赖
```
cd blog && npm install
```
- 启动服务
```
hexo server
```
#### 部署到github上
- 一个账号只能部署一个,名字必须交 用户名.github.io
- 发布github需要一个发布到github的插件
```
npm install hexo-deployer-git --save
```
- 配置发布文件
```
deploy:
  type: git
  repo: https://username:password@github.com/zuyuan/zuyuan.github.io.git
  branch: master
```
- 发布(每次更新都要执行这两部)
```
hexo g 生成
hexo d 发布
```
#### yarn包管理器
- 相当于你把nrm use cnpm,支持缓存
```
npm install yarn -g
```
#####
- 初始化package.json
```
yarn init -y
yarn add jquery vue 
yarn add babel-core -dev
```