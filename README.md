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

Mac安装git `brew install git`

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
    thor@tiantian:~/Documents/GitTest$ git add two.txt fourDir/
    thor@tiantian:~/Documents/GitTest$ git status
    On branch master
    
    No commits yet
    
    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)
    
     new file:   fourDir/four_dir_one.txt
     new file:   one.txt
     new file:   two.txt
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
     three.txt
    
    ```

- 添加所有新建的

  ```
  thor@tiantian:~/Documents/GitTest$ git add .
  thor@tiantian:~/Documents/GitTest$ git status
  On branch master
  
  No commits yet
  
  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
  
  	new file:   fourDir/four_dir_one.txt
  	new file:   one.txt
  	new file:   three.txt
  	new file:   two.txt
  ```


## 进行一次commit操作

`git commit`命令

```
thor@tiantian:~/Documents/GitTest$ git commit -m "add four files"
[master (root-commit) b989dc2] add four files
 4 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 fourDir/four_dir_one.txt
 create mode 100644 one.txt
 create mode 100644 three.txt
 create mode 100644 two.txt
```

## `git commit` 命令简单介绍

- `git commit -m [message]`：提交暂存区到仓库区
- `git commit [file1] [file2] ... -m [message]`：提交暂存区的指定文件到仓库区
- `git commit -a`：提交工作区自上次commit之后的变化，直接到仓库区
- `git commit -v`：提交时显示所有diff信息
- `git commit --amend -m [message]`：使用一次新的commit，替代上一次提交。如果代码没有任何新变化，则用来改写上一次commit的提交信息
- `git commit --amend [file1] [file2] ...`： 重做上一次commit，并包括指定文件的新变化

## 查看一下提交记录

`git log`命令查看一下当前提交记录

```
thor@tiantian:~/Documents/GitTest$ git log
commit b989dc26fa089d76de381ace2e360d69ab60e9ea (HEAD -> master)
Author: dongdong.wu <withwudongdong@gmail.com>
Date:   Sun Mar 17 14:49:31 2019 +0800

    add four files
```

## `git log` 命令简单介绍

具体可以查看Git官网查看，下面我就简单列举我用过的。[官网地址](https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2)

- `git log`：会按提交时间列出所有的更新，最近的更新排在最上面
  - 添加参数`-n`：显示最近提交n次记录。如`git log -3`显示最近提交的三次记录
  - 添加参数`--since, --after`：仅显示指定时间之后的提交。时间格式：比如说具体的某一天（“2008-01-15”），或者是多久以前（“2 years 1 day 3 minutes ago”）。如`git log --after="2019.3.17"`显示2019年3月17日之后提交的
  - 添加参数`--until, --before`：仅显示指定时间之前的提交。
  - 添加参数`--author`：仅显示指定作者相关的提交。如：`git log --author="dongdong.wu"`
  - 添加参数`--committer`：仅显示指定提交者相关的提交。如：`git log --committer="dongdong.wu"`
  - [**提交者和作者的区别**](https://github.com/xhacker/GitProTips/blob/master/zh_CN.md)
  - 添加参数`-p`：展开显示每次提交的内容差异。如`git log -p -1`显示最近一次提交的变化差异。该选项除了显示基本信息之外，还在附带了每次 commit 的变化。当进行代码审查，或者快速浏览某个搭档提交的 commit 的变化的时候，这个参数就非常有用了。
  - 添加参数`--stat`：仅显示简要的增改行数统计
  - 添加参数`--pretty`：可以指定使用完全不同于默认格式的方式展示提交历史
    - 一般用的参数`--pretty:format"一些参数具体看官网参数说明"`。例如：`$ git log --pretty=format:"%h - %an, %ar : %s"`
  - 添加参数`--online`：`--pretty=oneline --abbrev-commit` 的简化用法。
  - 添加参数`--graph`：显示 ASCII 图形表示的分支合并历史。



至此一次简单的git提交就完成了。

# git修改文件名称

## 第一种笨方法

```
# 第一步查看当前文件夹下有哪些文件
thor@tiantian:~/Documents/GitTest$ ls
fourDir  one.txt  three.txt  two.txt

# 第二步，我要把one.txt 重名了为 one.md
thor@tiantian:~/Documents/GitTest$ mv one.txt one.md

# 第三步 看本地文件是否重命名成功
thor@tiantian:~/Documents/GitTest$ ls
fourDir  one.md  three.txt  two.txt

# 第四步 把新改的文件添加到暂存区
thor@tiantian:~/Documents/GitTest$ git add one.md

# 第五步 删除原来暂存区中的文件，即one.txt
thor@tiantian:~/Documents/GitTest$ git rm one.[按两下TAB键会有下面提示]
one.md   one.txt  
thor@tiantian:~/Documents/GitTest$ git rm one.txt
rm 'one.txt'

# 第六步 查看当前暂存区，可以可看到提示就是	renamed:    one.txt -> one.md
thor@tiantian:~/Documents/GitTest$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	renamed:    one.txt -> one.md

```

## 第二种方法（推荐）

1. 因为使用了第一种方法文件名已经被改变了，所以我们要先恢复到原来版本状态。首先先用`git reset --hard`命令重置暂存区与工作区，与上一次commit保持一致。

2. 然后通过`git status`可以看到改变的都被取消了。在通过`ls`命令可以看到文件名被恢复原来样子了。

3. 现在我们就通过一个简单命令实现第一种方法。`git mv one.txt one.md`就可以实现第一种方法效果

   ```
   thor@tiantian:~/Documents/GitTest$ git mv one.txt one.md
   thor@tiantian:~/Documents/GitTest$ git status
   On branch master
   Changes to be committed:
     (use "git reset HEAD <file>..." to unstage)
   
   	renamed:    one.txt -> one.md
   
   thor@tiantian:~/Documents/GitTest$ ls
   fourDir  one.md  three.txt  two.txt
   ```

  4. 提交变更

      ```
      thor@tiantian:~/Documents/GitTest$ git commit -m "mv one.txt to one.md"
      [master 218dc3b] mv one.txt to one.md
       1 file changed, 0 insertions(+), 0 deletions(-)
       rename one.txt => one.md (100%)
      thor@tiantian:~/Documents/GitTest$ git log
      commit 218dc3bf854ae9f21c335d45c7370a9d3bb5ebb3 (HEAD -> master)
      Author: dongdong.wu <withwudongdong@gmail.com>
      Date:   Sun Mar 17 19:47:08 2019 +0800
      
          mv one.txt to one.md
      
      commit b989dc26fa089d76de381ace2e360d69ab60e9ea
      Author: dongdong.wu <withwudongdong@gmail.com>
      Date:   Sun Mar 17 14:49:31 2019 +0800
      
          add four files
      ```

# `git reset` 命令简单介绍

- `git reset --hard`：重置暂存区与工作区，与上一次commit保持一致
- `git reset --hard HEAD^`：用`HEAD`表示当前版本，上一个版本就是`HEAD^`，当然往上100个版本写100个`^`比较容易数不过来，所以写成`HEAD~100`。
- ` git reset --hard [commitId]`：commitId可以通过`git log --graph --oneline`获取的commitId就是最短的id
