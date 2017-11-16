---
title: git命令
date: 2017-08-27 19:37:00
tags:
---
## 新建分支
git init 
git add *
git commit -m 'init'
git remote add origin https://github.com/xxxxxx.git
git push -u origin master
## 分支
![](/img/git1.png)
Git branch 查看当前分支
Git branch -a 查看远程分支和当前分支
Git branch test 建立新分支

![](/img/git2.png)
Git branch -d branchName 删除本地某分支
Git branch -r -d origin/branchName 删除远程分支
Git push origin: branchName 删除远程分支

## 查看分支之间的关系和commit日志
![](/img/git3.png)


git log --graph --decorate --oneline --simplify-by-decoration --all

说明：
--decorate 标记会让git log显示每个commit的引用(如:分支、tag等) 
--oneline 一行显示
--simplify-by-decoration 只显示被branch或tag引用的commit
--all 表示显示所有的branch，这里也可以选择，比如我指向显示分支ABC的关系，则将--all替换为branchA branchB branchC

## 查看更改
![](/img/git4.png)
Git show <commitId> 查看某次更改的内容，不填写提交ID的话，显示最近一次更改的内容，id通过git log查询


## 撤销更改
	    撤销本地修改
	   跟踪的文件撤销修改
	    git checkout .
	   未跟踪的文件撤销修改
	   git clean -n        查看将要清除的文件
	   git clean -df         删除未跟踪的文件

### 撤销暂存,暂存的文件取消暂存变成已修改未暂存
Git reset HEAD b.txt
![](/img/git5.png)


### 更改commit提交信息
Git commit --amend进入编辑器更改提交信息
或者
Git commit --amend -m <newTips>
![](/img/git6.png)
将提交信息由change b 更改为change b.txt,
将提交信息由change b.txt更改为rechange b.txt

### 撤销提交(commit)文件
Git reset --hard <sha>
![](/img/git7.png)
Rechange b.txt的更改全部丢弃，本地也没有修改的文件

Git reset <sha>
![](/img/git8.png)
reset后修改的文件仍然保留在本地磁盘
### 在撤销commit后再恢复
reset后又还是想commit刚刚撤销的文件
Git reflog 
Git cherry-pick <sha>
查看HEAD改变的历史记录，它涉及的只是 HEAD 的改变。在你切换分支、用 git commit 进行提交、以及用 git reset 撤销 commit 时，HEAD 会改变，但当你用  git checkout -- <bad filename> 撤销时，HEAD 并不会改变 — 如前所述，这些修改从来没有被提交过，因此 reflog 也无法帮助我们恢复它们。
![](/img/git9.png)

### 撤销merge
道理同撤销commit一样
Git reset --hard <sha>
如果merge出现冲突的话
Git merge --abort
### 撤销已经push的内容
Git revert HEAD       撤销前一次push
Git revert HEAD^       撤销前前一次push
Git revert <sha>       
但是并不是之前提交的东西在分支上没有，还是会有记录的，另外假如后悔revert后，可以再revert一遍…
![](/img/git10.png)

## 合并分支
### rebase和merge的区别

## tag
### 查看tag
#### 查看所有tag
>git tag

按字母排序列出tag
#### 查看限定tag
>git tag -l 1.*
列出tag为1.0或者1.1等等版本
### 打tag
>git tag 1.0

### 给过去提交的代码打tag
>git log --oneline
git tag -a 0.1 

![](/img/git12.png '需要输入commit message否则不能打tag')
### 删除tag
>git tag -d 1.0

不用切换至tag那一条提交记录，直接删除即可
### push tag
>git push origin --tags

将tag上传到服务器