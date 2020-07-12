# Git的一个

### 小练习

## 加油！

### 此Git练习根据[廖雪峰Git教程](http://www.liaoxuefeng.com)上摘抄下来的，最后的英文pdf看不懂，所以写了这个

### git init

将当前目录转换成git管理的目录

会在当前目录生成.git文件夹

### git add FileName

添加文件到暂存区（也可以理解为中转站），

当FileName为.或*时提交全部。

### git commit \-m "注释"

提交暂存区的文件，一并提交！

建议写上注释，因为这样可以有效的帮助你~~少脱发~~。

### git status

~~监视~~你的文件修改了没有，简单的说就是文件夹里的文件和提交后的文件有没有区别。

如果修改了文件夹里的文件，会发出一串红色的~~光芒~~文字。

### git diff

查看你到底修改了什么内容，会显示文件夹里的文件和提交时的文件增加了什么，减少了什么。

### git log

查看最近提交的版本信息，什么时候提交了，版本号是什么。。。

commit: xxxxxxxx

xxxxx是版本号，记住前几位，以后版本回退时会用到它。

---

## 版本回退

### git reset \-\-hard HEAD^

退回上一个版本，

HEAD^^为上上一个版本，

HEAD~100退回前100个版本。。。

### git reset \-\-hard 版本号

退回到哪一个版本，版本号不用写全，写前四五位就可以了。

### git reflog

如果你退回后又想重新还原回来，可是你现在电脑已经关机，使用它，~~金坷垃~~。

可以显示你每一次命令。

### git diff HEAD \-\- xxx.txt

查看提交后和现在的文件有什么区别。

### git checkout \-\- xxx.txt

撤销在工作区的修改，文件名：xxx.txt

### git reset HEAD xxx.txt

撤销暂存区的修改，文件名：xxx.txt

### git rm xxx.txt

删除一个文件，与直接删的话，git status会告诉你删除文件。

使用git rm xxx.txt

再add，commit

删错了使用git checkout -- xxx.txt还原。

---

## 远程库

## ssh-keygen -t rsa -C "youremail@example.com"

在用户目录下生成.ssh，在id_rsa.pub下复制内容，然后在GitHub添加SSH，添加复制的内容，id_rsa是私钥文件，不能透露。

创建GitHub远程库后输入：git pull https://github.com/你的GitHub用户名/你的GitHub仓库名.git

然后输入：git remote add origin git@github.com:xxx/xxx.git

再输入git push -u origin master

这时候你打开GitHub就可以看见了。

以后在提交直接使用git push origin master

## git clone git@github.com:xxx/xxx.git

克隆仓库到当前文件夹。

---

## 分支管理

### git checkout -b dev

创建dev分支并切换。

同等于：

git branch dev

创建分支。

git checkout dev

切换分支。

### git branch

查看所有分支。

### git merge dev

合并分支，但前提是需要不在dev分支。

### git switch

git switch -c dev创建and切换分支。

git switch dev切换分支。

git branch -d dev

删除dev分支。

### 冲突

当两个分支合并时存在冲突，（如master和dev上的1.txt不同）则git则会这样：

```
<<<<<<< HEAD
xxx
=======
xxx
>>>>>>>
```

dev用`git log --graph`命令可以看到分支合并图。

可以加上`--pretty=oneline`和`--abbrev-commit`参数，

一个是漂亮的一条线，另一个是缩写commit。

### Fast forward

通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

添加--no-ff参数，就那么简单。

### 保存工作现场

git stash储藏当前工作环境。

用`git status`查看工作区，就是干净的（除非有没有被Git管理的文件）。

git stash list查看储存的环境。

一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；

另一种方式是用`git stash pop`，恢复的同时把stash内容也删了。

你可以多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令：

```
$ git stash apply stash@{0}
```

Git专门提供了一个`cherry-pick`命令，让我们能复制一个特定的提交到当前分支。

```
git cherry-pick 34x6a35
```


### 删除没有合并的分支

如果分支没有第一次合并，那么，要使用大写的D

```
git branch -D xxx
```


### 推送分支

git remote查看远程库的信息。

git remote -v显示更详细的信息。

git push origin master推送master分支，

当然，你也可以推送其他分支。

你也可以不推送其他分支，完全可以在家里玩。

### rebase

rebase可以将Git的提交历史变为一条干净的直线。

```
$ git rebas
```



中间输出了一大堆操作，在使用log一看，一条干净的直线，爽！

---

## 标签

### 标签管理

git打标签（不是你想的那个**打**标签）很简单：

首先，切换到需要打标签的分支，

再输入：

git tag v1.0

这样，这个分支就被打标签了😝

使用git tag查看标签。

也可以打在提交的commit上：

```
$ git tag v0.9 f52c633
```
可以用`git show <tagName>`查看标签信息。

也可以创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字：


```
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```


git tag -d v1.0删除标签


### 推送标签

git push origin v1.0推送标签，

git push origin --tags一口气推送全部标签。

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除，然后，从远程删除。删除命令也是push，但是格式如下：

>   ```
>$ git push origin :refs/tags/v0.9
>   ```
>要看看是否真的从远程库删除了标签，可以登陆GitHub查看。

## 使用GitHub

这个传说中最大的开源代码管理库和git有着什么样的关联呢？一起来学习吧！

### 如何提交/修改仓库文件

我们比如说李华现在有一个重要文件给晓东修改，提交到github仓库中（别问我为什么不用网盘），晓东现在该怎么做呢？

1.  打开李华提交的仓库，选择fork
2.  发现晓东也有了这个仓库，修改错误，产生一个pull request，等待李华同意

## 使用gitee

gitee（码云）是和GitHub相似的代码管理库。由于服务器在中国，下载，提交，界面都有了很大的变化。和GitHub一样，也是使用git，相当于一个国内版的GitHub

直接关联，会发现一个错误：

```
git remote add origin git@gitee.com:xxx/xxx.git
fatal: remote origin already exists.
```

原因是一个git不能关联两个名字为origin的仓库，查看一下：

```
git remote -v
origin	git@github.com:xxx/xxx.git (fetch)
origin	git@github.com:xxx/xxx.git (push)
```

这时，我们删除原有的仓库：

```
git rm origin
```

再关联gitee的仓库，就👌了

如果既能关联gitee，又可以关联gitee呢？

这时，差点荒废的origin终于派上用场了！

先关联GitHub的远程库：

```
git remote add github git@github.com:michaelliao/learngit.git
```

注意，远程库的名称叫`github`，不叫`origin`了。

接着，再关联Gitee的远程库：

```
git remote add gitee git@gitee.com:liaoxuefeng/learngit.git
```

同样注意，远程库的名称叫`gitee`，不叫`origin`。

现在，我们用`git remote -v`查看远程库信息，可以看到两个远程库：

```
git remote -v
gitee	git@gitee.com:xxx/xxx.git (fetch)
gitee	git@gitee.com:xxx/xxx.git (push)
github	git@github.com:xxx/xxx.git (fetch)
github	git@github.com:xxx/xxx.git (push)
```

如果要推送到GitHub，使用命令：

```
git push github master
```

如果要推送到Gitee，使用命令：

```
git push gitee master
```

这样一来，我们的本地库就可以同时与多个远程库互相同步

## 配置git

这一节中，主要讲如何配置git，使git更加高效

比如，让Git显示颜色，会让命令输出看起来更醒目：

```
$ git config --global color.ui true
```

## 忽略特殊文件

我们每一次都会分别哪一个需要提交，哪一个不需要，如配置文件，系统文件，密码等

这时，`.gitignore`文件就派上了用场

新建文件，重命名为`.gitignore`，写入文件名，如`py[cod]`，`Desktop.ini`，就可以了

```
# Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

# Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist
build

# My configurations:
db.ini
deploy_key_rsa
```

如果要强制提交，忽略`.gitignore`，加上-f参数：

```
$ git add -f App.class
```

或者你发现，可能是`.gitignore`写得有问题，需要找出来到底哪个规则写错了，可以用`git check-ignore`命令检查：

```
$ git check-ignore -v App.class
.gitignore:3:*.class	App.class
```

Git会告诉我们，`.gitignore`的第3行规则忽略了该文件，于是我们就可以知道应该修订哪个规则。

## 配置别名

为了方便，我们可以将一个命令缩写，如将status缩写成st：

```
$ git config --global alias.st status
```

`--global`参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。

在[撤销修改](https://www.liaoxuefeng.com/wiki/896043488029600/897889638509536)一节中，我们知道，命令`git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个`unstage`别名：

```
$ git config --global alias.unstage 'reset HEAD'
```

当你敲入命令：

```
$ git unstage test.py
```

实际上Git执行的是：

```
$ git reset HEAD test.py
```

配置一个`git last`，让其显示最后一次提交信息：

```
$ git config --global alias.last 'log -1'
```

这样，用`git last`就能显示最近一次的提交：

```
$ git last
commit adca45d317e6d8a4b23f9811c3d7b7f0f180bfe2
Merge: bd6ae48 291bea8
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Thu Aug 22 22:49:22 2013 +0800

    merge & fix hello.py
```

甚至还有人丧心病狂地把`lg`配置成了：

```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

来看看`git lg`的效果：

![git-lg](https://www.liaoxuefeng.com/files/attachments/919059728302912/0)

为什么不早点告诉我？别激动，咱不是为了多记几个英文单词嘛！

### 配置文件

配置Git的时候，加上`--global`是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

配置文件放哪了？每个仓库的Git配置文件都放在`.git/config`文件中：

```
$ cat .git/config 
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:xxx/xxx.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1
```

别名就在`[alias]`后面，要删除别名，直接把对应的行删掉即可。

而当前用户的Git配置文件放在用户主目录下的一个隐藏文件`.gitconfig`中：

```
$ cat .gitconfig
[alias]
    co = checkout
    ci = commit
    br = branch
    st = status
[user]
    name = Your Name
    email = your@email.com
```

配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。

## 使用SourceTree

SourceTree是一个非常好的git图形化的软件，

进入[官网](https://www.sourcetreeapp.com/)下载即可。

因为我很懒，没有很多文件，也将这个很多省略，因为这个时候很晚了。

完事！