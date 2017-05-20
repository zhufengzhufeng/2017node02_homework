## git remote
git clone 自己的项目地址
添加内容
git add .
git commit -m 'team xxx'
git remote add leader 组长的地址（建立一次即可）
git pull leader master
git push origin master


e.g.
fork --等待-->复制到自己的库（点击进入复制已生成的地址）

            ——>git clone https://github.com/honghong812128/2017node02_homework.git homework
                (git clone 自己的项目地址 文件夹名)

            -->(此时本地已经下载了库里的文件,git 切换到homework中)

            -->git add .

            -->git commit -m 'log message'

            -->git remote add homework https://github.com/TonyShan2016/2017node02_homework.git
               (git remote add leader 组长的地址（建立一次即可）)
               leader 为自定义的属于自己的分支名称

            -->git pull homework master
                (先拉取后提交)

            -->git push origin master
                (此时将更改的代码提交到自己github种相应的库)

            -->new pull request
                (提交请求)


