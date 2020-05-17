# Git的一个

### ~~小练习~~ 学习

## 希望能将Git引进~~学校~~，~~公司~~，甚至替代~~某网盘~~

## 加油！

### git init

>   将当前目录转换成git管理的目录
>   会在当前目录生成.git文件夹

### git add FileName

>   添加文件到暂存区（也可以理解为中转站）
>
>   当FileName为.或*时提交全部

### git commit \-m "注释"

>   提交暂存区的文件，一并提交！
>
>   建议写上注释，因为这样可以有效的帮助你~~少脱发~~

### git status

>   ~~监视~~你的文件修改了没有，简单的说就是文件夹里的文件和提交后的文件有没有区别
>
>   如果修改了文件夹里的文件，会发出一串红色的~~光芒…~~文字

### git diff

>   查看你到底修改了什么内容，会显示文件夹里的文件和提交时的文件增加了什么，减少了什么

### git log

>   查看最近提交的版本信息，什么时候提交了，版本号是什么。。。
>
>   commit: xxxxxxxx
>
>   xxxxx是版本号，记住前几位，以后版本回退时会用到它

## 版本回退

### git reset \-\-hard HEAD^

>   退回上一个版本
>
>   HEAD^^为上上一个版本
>
>   HEAD~100退回前100个版本。。。

### git reset \-\-hard 版本号

>   退回到哪一个版本，版本号不用写全，写前四五位就可以了

### git reflog

>   如果你退回后又想重新还原回来，可是你现在电脑已经关机，使用它，~~金坷垃~~
>
>   可以显示你每一次命令

### git diff HEAD \-\- xxx.txt

>   查看提交后和现在的文件有什么区别

### git checkout \-\- xxx.txt

>   撤销在工作区的修改，文件名：xxx.txt

### git reset HEAD xxx.txt

>   撤销暂存区的修改，文件名：xxx.txt

### git rm xxx.txt

>   删除一个文件，与直接删的话，git status会告诉你删除文件
>
>   使用git rm xxx.txt
>
>   再add，commit
>
>   删错了使用git checkout -- xxx.txt还原

## 远程库

## ssh-keygen -t rsa -C "youremail@example.com"

>   在用户目录下生成.ssh，在id_rsa.pub下复制内容，然后在GitHub添加SSH，添加复制的内容，id_rsa是私钥文件，不能透露
>
>   创建GitHub远程库后输入：git pull https://github.com/你的GitHub用户名/你的GitHub仓库名.git
>
>   然后输入：git remote add origin git@github.com:xxx/xxx.git
>
>   在输入git push -u origin master
>
>   这时候你打开GitHub就可以看见了
>
>   以后在提交直接使用git push origin master
>
## git clone git@github.com:xxx/xxx.git

>   克隆仓库到当前文件夹

## 分支管理

### git checkout -b dev

>   创建dev分支并切换
>
>   同等于：
>
>   git branch dev
>
>   创建分支
>
>   git checkout dev
>
>   切换分支

### git branch

>   查看所有分支

### git merge dev

>   合并分支，但前提是需要不在dev分支

## git switch

>   git switch -c dev创建and切换分支
>
>   git switch dev切换分支

git branch -d dev

>   删除dev分支

## 冲突

## 