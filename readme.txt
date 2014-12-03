#初始化
git init
#添加到版本库
git add .
git commit -m
#查看库中状态
git status
#比较文件不同
git diff
#版本回退
git reset --hard HEAD^ or HEAD^^ or HEAD~100
#查看日志
git log
git reflog

#工作区和暂存区
.git 是git的版本库其中最重要的称为stage(index)的暂存区,还有git自动创建的第一个分支master,以及指向master的一个HEAD指针

git add 实际上是将文件修改添加到暂存区
git commit 实际上是将暂存区的所有内容提交到当前分支上

#与其他版本控制器的区别
git跟踪并管理的是修改,而非文件

#撤销修改
git checkout -- readme.txt 将工作去的该文件的修改撤销
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

"--" 符号必须存在, 否则git checkout 命令变成 创建一个新分支的命令

git reset HEAD file 撤销暂存区的修改unstage

#删除文件
git rm, 只能恢复到最新文件, 最近一次提交之后的修改内容将丢失,所以提交到版本库,比较不用担心误删


#远程仓库
Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。怎么分布呢？最早，肯定只有一台机器有一个原始版本库，此后，别的机器可以“克隆”这个原始版本库，而且每台机器的版本库其实都是一样的，并没有主次之分

其实一台电脑上也是可以克隆多个版本库的，只要不在同一个目录下,并且没有必要,可以使用github作为远程仓库,就是github上放自己的远程库和本地库进行传输

git仓库和github仓库之间的传输是通过ssh加密的需要设置
1. 窗将ssh key
查看～/.ssh下有没有id_rsa私钥和id_rsa.pub共钥, 没有的化
ssh-keygen -t rsa -C "email@example.com"
一路enter,默认设置即可

2.第2步：登陆GitHub，打开“Account settings”，“SSH Keys

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：


为什么github需要ssh key?
GitHub需要识别出你推送的提交确实是你推送的
GitHub允许你添加多个Key,可能你在多台机子上有库

#新建远程仓库
…or create a new repository on the command line
touch README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/basiljava00/test.git
git push -u origin master

将本地库推送到远程仓库
…or push an existing repository from the command line
git remote add origin https://github.com/basiljava00/test.git
git push -u origin master
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
