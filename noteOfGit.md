---
title: "Git"
date: 2021-04-25T08:53:10+08:00
draft: false
---

# Git 学习笔记 

## Git 简介
* 分布式版本控制系统
* 记录每次的改动同时保留每次的版本，允许多人协作   
* 由C语言开发  
* CVS（最早的开源而且免费的集中式版本控制系统，漏洞多，提交的文件会不完整）及SVN（更稳定）都是集中式的版本控制系统

### 分布式与集中式的区别
* 集中式版本控制系统
	+ 版本库集中存放在中央服务器
	+ 需要对版本进行修改时需要先从中央服务器获取，再进行修改，最后提交到中央服务器
	+ 必须联网才能够工作
* 分布式版本控制系统
	+ 没有中央服务器的概念，每个人的电脑都是一个独立的版本库
	+ 安全性更高，没有中央服务器依旧可以继续工作
	+ 分布式的“中央服务器”是为了方便大家交换版本修改
	+ 分支管理
* BitKeeper, Mercurial和Bazaar   

### 创建版本库
* mkdir：用于创建目录 mkdir [路径名]
* pwd：用于显示现在的路径
* git init (将当前目录变成Git可以管理的仓库)
	+ 会出现一个.git文件，但是该文件是隐藏的，利用ls -ah文件可以看到路径
* 所有的版本控制系统，其实只能跟踪文本文件的改动，对于视频、图片等二进制文件的改动，只能知道改了什么东西，但不会知道具体的内容
### 添加文件
1. git add **.**  //将文件添加到Git仓库
   * 要先有才能添加
   * 可以add 很多文件，用commit一次全部提交
2. git commit -m "this is a commit"
   * 作用是将文件提交到仓库
   * -m 后面的" "里面的内容是对提交的文件的简单说明
   *  
    	$ git commit -m "my tst"  
    	[master (root-commit) 6ccf4f2] my tst  
     	1 file changed, 0 insertions(+), 0 deletions(-)  
    	create mode 100644 hi.txt  

		1 file changed ---> 一个文件发生改变  
		0 insertions(+), 0 deletions(-) -----> 表示文件的数目加减
	* git命令必须在Git仓库目录下使用    
### 文件修改
1. git status
	* 显示仓库的文件修改状态
	* 未add的新创建的文件、修改未add的文件、已经add等待commit的文件（untracked）
2. git diff 
	* 显示仓库修改的具体内容
3. 提交修改和提交新文件的操作是一样的

### 版本回退
1. git log 
	* 用来查看自己的修改记录
	* commmit 后跟着的是commit id 
	* git log --pretty=oneline
		* 显示为一条时间线的形式
		* HEAD 表示当前版本
2. git reset --hard HEAD^
	* HEAD^ 可以替换为任意想要退回的版本，^的数目代表是往前数第几个版本，数目大的话换HEAD~100
	* 如果想要再换回退回之前的版本（主要就是查找原来的版本号）
		* 如果命令窗口还没有关闭可以直接找到版本号
		* 否则通过 git reflog 查看命令历史，可以找到之前的版本号

### 工作区与暂存区
1. 工作区（Working Directory）  
   电脑内可见目录
2. 版本库（Repository）  
   * 隐藏目录.git  
		* stage/index 暂存区
		* master 
		* 指向master的一个指针HEAD
	* git add 是把文件添加到暂存区
	* git commit 是将暂存区内的所有内容提交到当前分支

### 管理修改
**Git跟踪并管理的是修改，而非文件**  
如果git add之后还没有cmmit又修改了文件，修改的内容荣并不会同步到git add的版本之中，除非再一次git add，相当于将两次修改合并，是一次记录

### 撤销修改  
* git restore \<file>
	只是修改了，还没有add，撤回到上一次添加暂存区之后的状态（工作区修改全部丢弃）
* git restore --staged \<file>
	撤回的是add操作，将文件在暂存区的内容清空
* 已经commit但是还没有提交到远程库，版本回退即可（git reset --hard \<file>）

### 删除文件
* 直接删除
* rm 命令 git rm \<file>
* 恢复使用git restore \<file>，如果直接从回收站恢复相当于重新搞了一个文件需要重新add 和 commit  

### 远程仓库
* ssh-keygen -t rsa -C "3148366342@qq.com"  创建SSH key
	ssh key 的作用是为了让Github识别自己的推送  
	允许添加多个key
### 添加远程仓库
1. 在githu创建新的仓库
2. 