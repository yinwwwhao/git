# Git的一个

### 小练习

## 加油！

### 此Git练习根据[廖雪峰Git教程](http://www.liaoxuefeng.com)上摘抄下来的，最后的英文pdf看不懂，所以写了这个

### git init

>   将当前目录转换成git管理的目录
>   
>   会在当前目录生成.git文件夹

### git add FileName

>   添加文件到暂存区（也可以理解为中转站），
>
>   当FileName为.或*时提交全部。

### git commit \-m "注释"

>   提交暂存区的文件，一并提交！
>
>   建议写上注释，因为这样可以有效的帮助你~~少脱发~~。

### git status

>   ~~监视~~你的文件修改了没有，简单的说就是文件夹里的文件和提交后的文件有没有区别。
>
>   如果修改了文件夹里的文件，会发出一串红色的~~光芒~~文字。

### git diff

>   查看你到底修改了什么内容，会显示文件夹里的文件和提交时的文件增加了什么，减少了什么。

### git log

>   查看最近提交的版本信息，什么时候提交了，版本号是什么。。。
>
>   commit: xxxxxxxx
>
>   xxxxx是版本号，记住前几位，以后版本回退时会用到它。

---

## 版本回退

### git reset \-\-hard HEAD^

>   退回上一个版本，
>
>   HEAD^^为上上一个版本，
>
>   HEAD~100退回前100个版本。。。

### git reset \-\-hard 版本号

>   退回到哪一个版本，版本号不用写全，写前四五位就可以了。

### git reflog

>   如果你退回后又想重新还原回来，可是你现在电脑已经关机，使用它，~~金坷垃~~。
>
>   可以显示你每一次命令。

### git diff HEAD \-\- xxx.txt

>   查看提交后和现在的文件有什么区别。

### git checkout \-\- xxx.txt

>   撤销在工作区的修改，文件名：xxx.txt

### git reset HEAD xxx.txt

>   撤销暂存区的修改，文件名：xxx.txt

### git rm xxx.txt

>   删除一个文件，与直接删的话，git status会告诉你删除文件。
>
>   使用git rm xxx.txt
>
>   再add，commit
>
>   删错了使用git checkout -- xxx.txt还原。

---

## 远程库

## ssh-keygen -t rsa -C "youremail@example.com"

>   在用户目录下生成.ssh，在id_rsa.pub下复制内容，然后在GitHub添加SSH，添加复制的内容，id_rsa是私钥文件，不能透露。
>
>   创建GitHub远程库后输入：git pull https://github.com/你的GitHub用户名/你的GitHub仓库名.git
>
>   然后输入：git remote add origin git@github.com:xxx/xxx.git
>
>   在输入git push -u origin master
>
>   这时候你打开GitHub就可以看见了。
>
>   以后在提交直接使用git push origin master
>
## git clone git@github.com:xxx/xxx.git

>   克隆仓库到当前文件夹。

---

## 分支管理

### git checkout -b dev

>   创建dev分支并切换。
>
>   同等于：
>
>   git branch dev
>
>   创建分支。
>
>   git checkout dev
>
>   切换分支。

### git branch

>   查看所有分支。

### git merge dev

>   合并分支，但前提是需要不在dev分支。

### git switch

>   git switch -c dev创建and切换分支。
>
>   git switch dev切换分支。

git branch -d dev

>   删除dev分支。

### 冲突

>   当两个分支合并时存在冲突，（如master和dev上的1.txt不同）则git则会这样：
>
>   ```
>   <<<<<<< HEAD
>   xxx
>   =======
>   xxx
>   >>>>>>> dev
>   ```
>
>   用`git log --graph`命令可以看到分支合并图。
>
>   可以加上`--pretty=oneline`和`--abbrev-commit`参数，
>
>   一个是漂亮的一条线，另一个是缩写commit。

### Fast forward

>   通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。
>
>   如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
>
>   添加--no-ff参数，就那么简单。

### 保存工作现场

>   git stash储藏当前工作环境。
>
>   用`git status`查看工作区，就是干净的（除非有没有被Git管理的文件）。
>
>   git stash list查看储存的环境。
>
>   一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；
>
>   另一种方式是用`git stash pop`，恢复的同时把stash内容也删了。
>
>   你可以多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令：
>
>   ```
>   $ git stash apply stash@{0}
>   ```
>
>   Git专门提供了一个`cherry-pick`命令，让我们能复制一个特定的提交到当前分支。
>
>   ```
>   git cherry-pick 34x6a35
>   ```
>

### 删除没有合并的分支

>   如果分支没有第一次合并，那么，要使用大写的D
>   
>   ```
>   git branch -D xxx
>   ```
>   

### 推送分支

>   git remote查看远程库的信息。
>
>   git remote -v显示更详细的信息。
>
>   git push origin master推送master分支，
>
>   当然，你也可以推送其他分支。
>
>   你也可以不推送其他分支，完全可以在家里玩。

### rebase

>   rebase可以将Git的提交历史变为一条干净的直线。
>
>   ```
>   $ git rebase
>   ```
>
>   中间输出了一大堆操作，在使用log一看，一条干净的直线，爽！

---

## 标签

### 标签管理

>   git打标签（不是你想的那个**打**标签）很简单：
>
>   首先，切换到需要打标签的分支，
>
>   再输入：
>
>   git tag v1.0
>
>   这样，这个分支就被打标签了😝
>
>   这些Microsoft中文输入法的表情符号我永远不会忘记，因为：
>
>   Bing: 我不会说中文，但我会英语和表情符号，流利的表情符号😝
>
>   使用git tag查看标签。
>
>   也可以打在提交的commit上：
>
>   ```
>   $ git tag v0.9 f52c633
>   ```
>
>   可以用`git show <tagName>`查看标签信息。
>   	
>   还可以创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字：
>
>   ```
>   $ git tag -a v0.1 -m "version 0.1 released" 1094adb
>   ```
>
>   
>   git tag -d v1.0删除标签
>   

### 推送标签

>   不是你们想的flash插件推送😝
>
>   git push origin v1.0推送标签，
>
>   git push origin --tags一口气推送全部标签。
>
>   如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除，然后，从远程删除。删除命令也是push，但是格式如下：
>
>   ```
>   $ git push origin :refs/tags/v0.9
>   ```

