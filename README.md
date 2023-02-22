# GitTest - A test project for project management via Github

## I. 简介

## II. 工作原理

## III. 具体操作

### A. 关联个人电脑（PC）与Github账户

Git并不像[SVN](https://subversion.apache.org/)那样有个中心服务器。目前我们使用到的Git命令都是在本地执行，比如你想通过Git分享你的代码或者与其他开发人员合作进行项目开发，又比如你有多台PC或者多个工作地点，想实现项目版本更新同步，你就需要将数据放到一台其他开发人员或其他PC能够连接的服务器上。为了方便项目开发及代码管理，在Github上建立远程仓库是十分明智的选择。

为了方便利用Github进行项目管理，我们可以先建立PC与对应Github账户之间的连接。由于本地Git仓库和GitHub远程仓库之间的传输是通过SSH加密的，所以我们需要配置验证信息。首先，我们可以使用以下命令在本地生成SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

标签-C后面的内容为注释，为了方便区分，可以把```your_email@youremail.com```改为个人的Github账号（当然，不管也是没问题的）。之后会要求确认路径和输入密码，在此只需一直回车选择默认选项就行，就像这样：

```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/liusongwei/.ssh/id_rsa_github):
Enter passphrase (empty for no passphrase):   
Enter same passphrase again: 
Your identification has been saved in /Users/liusongwei/.ssh/id_rsa_github
Your public key has been saved in /Users/liusongwei/.ssh/id_rsa_github.pub
The key fingerprint is:
SHA256:GTFbdl7uJAnG4tmCmH/frOIbM1JCAO1g5YuowSmXXg8 sl4417@columbia.edu
The key's randomart image is:
+---[RSA 3072]----+
|  .+o   o.= . .  |
|  o...  .B.+ +   |
| . o.o.oo+  + o  |
|...o+o. +o.  +   |
|+o+ E.. S.    .  |
|o+ . o.o.        |
|. .   o.+. o     |
|       ..+. o    |
|       .oo..     |
+----[SHA256]-----+
```



成功的话会在~/下生成.ssh文件夹，里面存放着私钥（id_rsa）和公钥（id_rsa.pub）。 利用记事本打开 id_rsa.pub，复制里面的公钥并上传到Github即可。详细操作可见这篇博文：[如何使用SSH连接到Github](https://zhuanlan.zhihu.com/p/111344840)。然后，我们利用```ssh -T git@github.com```命令与Github连接即可。首次连接会返回以下信息：

如果已经连接成功再执行```ssh -T git@github.com```命令，则会返回以下信息：
```
$ ssh -T git@github.com
Hi MajestyV! You've successfully authenticated, but GitHub does not provide shell access.
```

### B. Managing project? (not yield decided)

### X. 上传代码到Github远程仓库

首先，git add要上传的文件或者目录到暂存区：

```
$ git add [file1] [file2] ...  # 添加一个或多个文件到暂存区
$ git add [dir]                # 添加指定目录到暂存区，包括其子目录
$ git add .                    # 添加当前目录下的所有文件到暂存区
```

然后，利用git commit命令将暂存区内容添加到本地仓库中：

```
$ git commit -m [message]      # 标签-m后面可以写上本次提交的备注信息
```

最后，上传代码到远程仓库并合并：

```
$ git push
```

有时，本地仓库和远程仓库会存在版本冲突问题，例如：

```
To github.com:MajestyV/GitTest.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'github.com:MajestyV/GitTest.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

可以先git pull拉取远程仓库的最新版本融合到本地，再重新上传一次代码（即重复上述操作）。更多问题，可以参考这篇博文：[Git push 时如何避免出现 "Merge branch 'master' of ..."](https://www.cnblogs.com/Sinte-Beuve/p/9195018.html).

## IV. 常用命令行详解

### (X) git pull - 下载远程代码并合并
git pull 命令用于从远程获取代码并合并本地的版本。git pull 其实就是 git fetch 和 git merge FETCH_HEAD 的简写。

```
$ git pull <远程主机名> <远程分支名>:<本地分支名>
```

### (X) git push - 	上传远程代码并合并

git push 命令用于从将本地的分支版本上传到远程并合并。

```
$ git push <远程主机名> <本地分支名>:<远程分支名>
```

如果本地分支名与远程分支名相同，则可以省略冒号:

```
$ git push <远程主机名> <本地分支名>
```

### (X) git

## 外部链接

### A. 关于SSH

[X] [安全外壳协议（Secure Shell Protocol，简称SSH）- 维基百科](https://zh.wikipedia.org/wiki/Secure_Shell)

[X] [SSH 免密登录是怎么玩儿的?](https://zhuanlan.zhihu.com/p/28423720)

### B. 关于Git

[1] [Git官网](https://git-scm.com/)

[X] [Git教程 - 菜鸟教程](https://www.runoob.com/git/git-tutorial.html)

### C. 关于Github

[1] [Github官网](https://github.com/)

[2] [Github中文操作手册（可谓包罗万有）](https://docs.github.com/zh/get-started)

[X] [Github简明教程 - 菜鸟教程](https://www.runoob.com/w3cnote/git-guide.html)

### D. 利用Github进行项目代码管理

[1] [关于Github存储库](https://docs.github.com/zh/repositories)
