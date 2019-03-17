[TOC]

# Git学习整理

> 更新2019-3-17
>
> 学习自  
> [极客时间-玩转Git三剑客](https://time.geekbang.org/course/intro/145)   
> [Git官网](https://git-scm.com/)  
> [常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)  

# 安装Git

[官网安装教程](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

Windows打开`Git Bash`输入`git --version`查看当前安装git版本信息，如果是Mac直接打开命令行输入`git --version`。

# Git最小配置

```
git config --global user.name "dongdong.wu"
git config --global user.email "withwudongdong@gmail.com"
git config --global color.ui auto
```

## config的三个作用域

```
git config --local    //只针对某个仓库
git config --global	  //针对当前用户所有仓库
git config --system   //针对当前系统所有登录的用户
```

## 显示config的配置信息

```
git config --list
git config --list --local
git config --list --global
git config --list --system
```

也可以查看当前用户下的`.gitconfig`即

```
cd
cat .gitconfig
```

# 创建Git仓库

```
//1.创建一个新项目
mkdir GitTest
//2.初始化该项目
cd GitTest
git init  //执行完成后，提示Initialized empty Git repository in C:/Users/Thor/Desktop/GitTest/.git/
//3.查看是否初始化项目成功，用下面命令可以看到一个.git文件表示初始化成功
ls -al
```

# 提交认知

一般我们自己本地git在提交分为3个区域：

1. 我们自己的**工作目录**
2. `git add files`之后文件进入的**暂存区**
3. `git commit`之后文件进入的**版本历史**



如果有远程仓库，给Git正在的区域分布为下面四个区域：

- Workspace：工作区
- Index / Stage：暂存区
- Repository：仓库区（或本地仓库）
- Remote：远程仓库

下面图片来源为：[常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

![引用阮一峰的网络日志的图片](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png)

## 在GitTest添加四个文件

- `touch one.txt two.txt three.txt`创建三个文件，然后用`ls`查看当前目录下是否有这四个文件。
- `mkdir four`创建一个文件夹，进入文件夹`cd four`，创建一个文件`touch four_dir_one.txt`

这样之后我们的四个文件都创建好了。

##  查看当前工作目录与暂存区的关系

`git status`，输入当前命令可以看到下面提示。

```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	fourDir/
	one.txt
	three.txt
	two.txt

nothing added to commit but untracked files present (use "git add" to track)
```

告诉我们下面这四个文件git从来没有管理过，那怎么可以管理呢？可以看到上面提示中已经给出我们答案了`git add 文件`就可以添加管理了。

## `git add` 命令简单介绍

- `git add [file]`：将文件添加进暂存区
- `git add [file1] [file2] ...`：将多个文件添加进暂存区
- `git add -u`：将文件的修改、文件的删除，添加到暂存区。
- `git add .`：将文件的修改，文件的新建，添加到暂存区。
- `git add -A`：将文件的修改，文件的删除，文件的新建，添加到暂存区。
- `git add -u` 以及他们之间的区别
  `git add -A`相对于`git add -u`命令的优点 ： 可以提交所有被删除、被替换、被修改和新增的文件到数据暂存区，而`git add -u` 只能操作跟踪过的文件
  `git add -A `等同于`git add -all`

- `git add *Controller` ：将以Controller结尾的文件的所有修改添加到暂存区

- `git add Hello*` ：将所有以Hello开头的文件的修改添加到暂存区 例如:HelloWorld.txt,Hello.java,HelloGit.txt ...

- `git add Hello?` ：将以Hello开头后面只有一位的文件的修改提交到暂存区 例如:Hello1.txt,HelloA.java 如果是HelloGit.txt或者Hello.java是不会被添加的

简单的例子 

git add 可以直接后面加多个文件或文件夹

- 添加一个文件方式

    ```
    thor@tiantian:~/Documents/GitTest$ git add one.txt 
    thor@tiantian:~/Documents/GitTest$ git status
    On branch master
    
    No commits yet
    
    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
    
     new file:   one.txt
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
     fourDir/
     three.txt
     two.txt
    
    ```

- 添加多个文件

    ```
    thor@tiantian:~/Documents/GitTest$ git add two.txt 
