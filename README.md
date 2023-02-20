# GitTest - A test project for project management via Github

## I. 简介

## II. 工作流程

### A. 关联个人电脑（PC）与Github账户


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

## III. 常用命令行详解

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

### B. 关于Git

[1] [Git官网](https://git-scm.com/)

[X] [Git教程 - 菜鸟教程](https://www.runoob.com/git/git-tutorial.html)

### C. 关于Github

[1] [Github官网](https://github.com/)

[2] [Github中文操作手册（可谓包罗万有）](https://docs.github.com/zh/get-started)

[X] [Github简明教程 - 菜鸟教程](https://www.runoob.com/w3cnote/git-guide.html)

### D. 利用Github进行项目代码管理

[1] [关于Github存储库](https://docs.github.com/zh/repositories)