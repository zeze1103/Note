# Git Command

## Git config

```
git config --global user.name "Your name "
git config --global user.email "email@example.com"
```



```
git init	将当前文件夹创建仓库
```

所有的版本控制系统，其实只能跟踪文本文件的改动



## 添加一个文件到仓库

新建文件 readme.md

```
	git add readme.md
	git commit -m "xxxx"(备注)
```



## 查看状态

```
git status
git diff	查看究竟哪里被修改了
```



## 查看版本改动

```
git log
git log --pretty=oneline
git reflog 记录所有命令
```



## 回退版本

```
git reset --hard HEAD^	返回上一个版本
git reset --hard （版本hash值） 返回Hash对应版本
```



## 工作区与暂存区

![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)

`git add`把文件添加进去，实际上就是把文件修改添加到暂存区

`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支

`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别



## 撤销修改

`git checkout -- file`可以丢弃工作区的修改：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。



`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区

`git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。



场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)一节，不过前提是没有推送到远程库。





## 删除文件

```
rm test.txt
git rm test.txt
git commit -m "remove test.txt"
```

`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。



1.如果你用的rm删除文件，那就相当于只删除了工作区的文件，如果想要恢复，直接用git checkout -- file就可以 2.如果你用的是git rm删除文件，那就相当于不仅删除了文件，而且还添加到了暂存区，需要先git reset HEAD file，然后再git checkout -- file

 3.如果你想彻底把版本库的删除掉，先git rm，再git commit 





## 远程仓库

```
ssh-keygen -t rsa -C "youremail@example.com" 	创建shh Key

git remote add origin git@github.com:michaelliao/learngit.git	将本地的当前仓库下关联到新建的远程origin下

git push -u origin master	将本地master推送到远程origin	-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
git push origin master	将本地master推送到远程origin
```



## 分支管理

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并

#### 创建与合并分支

```
git checkout -b dev		创建dev分支，并切换到dev		-b参数表示创建并切换,相当于以下两条命令
git branch dev
git checkout dev
git branch 查看当前分支
git merge dev 将指定分支合并到当前分支
git branch -d dev 删除指定分支
```

#### 解决冲突

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

用`git log --graph`命令可以看到分支合并图

#### 分支管理策略	





