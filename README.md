# GitTutorial - A tutorial project for project management via Git

## I. 简介

[Git](https://git-scm.com/)并不像[SVN](https://subversion.apache.org/)那样有个中心服务器。目前我们使用到的Git命令都是在本地执行，比如你想通过Git分享你的代码或者与其他开发人员合作进行项目开发，又比如你有多台PC或者多个工作地点，想实现项目版本更新同步，你就需要将数据放到一台其他开发人员或其他PC能够连接的服务器上。无论是对于个人开发者亦或是开发团队，为了方便代码多地多人共同开发及项目管理，在[GitHub](https://github.com/)或者[GitLab](https://about.gitlab.com/)上建立远程仓库是十分明智的选择。

## II. 工作原理

Git 是一种分布式版本控制系统，广泛应用于项目管理和代码协作。其工作原理主要包括以下几个方面：

1. **版本管理**：Git 通过快照的方式记录项目文件的状态，每次提交（commit）都会生成一个唯一的版本号，方便开发者随时回溯和比较历史版本。
2. **分支管理**：Git 支持多分支开发，开发者可以在不同分支上并行工作，如功能开发、bug 修复等，分支之间互不干扰，最终可以通过合并（merge）将分支上的成果整合到主分支。
3. **分布式协作**：每个开发者都拥有完整的仓库副本，可以在本地进行开发和提交，不受网络限制。通过推送（push）和拉取（pull）操作，实现与远程仓库的数据同步，方便团队成员协作。
4. **冲突解决**：当多个开发者对同一文件进行修改时，Git 会检测到冲突，并要求开发者手动解决，确保代码的正确性和一致性。

通过上述机制，Git 能有效地帮助项目团队进行代码管理、协作开发和版本控制，提高项目开发效率和质量。

## III. Git使用教程

* [如何使用GitHub或GitLab进行项目管理](docs/如何使用GitHub或GitLab进行项目管理.md)

## IV. 具体操作

### A. 关联个人电脑（PC）与Github账户

为了方便利用Github进行项目管理，我们可以先建立PC与对应Github账户之间的连接。由于本地Git仓库和GitHub远程仓库之间的传输是通过SSH加密的，所以我们需要配置验证信息。首先，我们可以使用以下命令在本地生成SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

有时我们的本地机器可能会用到多个Git账号对于不同的项目或者是远程服务器，此时我们就需要不同的SSH Key来对应不同Git账号。但是如果我们已经有生成好的SSH Key文件又直接通过上述命令行来生成新Key，新的密钥就会把老的密钥覆盖掉。此时，我们就可以通过给密钥文件定义新的文件名加以区分：

```
$ ssh-keygen -t rsa -C "youremail@example.com" -f ~/.ssh/id_rsa_github
```

标签```-f```指定密钥文件存储文件名，利用```-f```标签，我们可以给密钥文件赋予新的文件名。关于一台本地终端如何配置多个SSH Key，更多细节可以参考这篇博文：[Mac上配置SSH - 多个SSH](https://www.jianshu.com/p/d29ef6aefee2)。标签```-t```指定密钥类型，默认是 rsa ，可以省略。标签```-C```后面的内容为注释，为了方便区分，可以把```your_email@youremail.com```改为个人的Github账号（当然，不管也是没问题的）。之后会要求确认路径和输入密码，在此只需一直回车选择默认选项就行，就像这样：

```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/liusongwei/.ssh/id_rsa):  # 首次生成SSH Key可选择密钥存放地址，对于健忘人士，建议直接回车
Enter passphrase (empty for no passphrase):                           # 登陆密码，对于健忘人士，建议直接回车不要密码
Enter same passphrase again:                                          # 如未设置密码，直接回车就好
Your identification has been saved in /Users/liusongwei/.ssh/id_rsa
Your public key has been saved in /Users/liusongwei/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:GTFbdl7uJAnG4tmCmH/frOIbM1JCAO1g5YuowSmXXg8 sl4417@columbia.edu
The key's randomart image is:
+---[RSA 3072]----+
|           . o   |
|   . .    . . +  |
|  . o . .  ... . |
|   o o o o o.+.  |
|  o . . E *.o.o. |
|   o . . +.B+o. .|
|    . . o.=+=o.o |
|       ..o ===o  |
|      ..  o+Bo   |
+----[SHA256]-----+
```

成功的话会在```~/```下生成```.ssh```文件夹，里面存放着私钥```id_rsa```和公钥```id_rsa.pub```。 利用记事本打开```id_rsa.pub```，复制里面的公钥并上传到Github即可。详细操作可见这篇博文：[如何使用SSH连接到Github](https://zhuanlan.zhihu.com/p/111344840)。接下来，我们还需激活与Github的连接，要完成这一步，只需在本地终端执行以下命令即可：

```
$ ssh -T git@github.com
Hi MajestyV! You've successfully authenticated, but GitHub does not provide shell access.
```

有时新的客户端初次连接Github时会显示这种警报：

```
$ ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ECDSA key fingerprint is SHA256:XXXXXXXXXXXXXXXXXX.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

这种情况下其实没有任何问题，就是应当注意不要直接回车（按```enter```)，要先输入```yes```再```enter```：

```
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ECDSA key fingerprint is SHA256:XXXXXXXXXXXXXXXXXX.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com,20.205.243.166' (ECDSA) to the list of known hosts.
Hi MajestyV! You've successfully authenticated, but GitHub does not provide shell access.
```

详情可以参考：[git使用--解决The authenticity of host ‘github.com (20.205.243.166)‘ can‘t be established](https://blog.csdn.net/mj_zm/article/details/120413479)。这类警报的原因是当前客户端为没有host关于Github网站的内容，所以出现问题。

### B. Managing project? (not yield decided)

### X. 上传代码到Github远程仓库

首先，```git add```要上传的文件或者目录到暂存区：

```
$ git add [file1] [file2] ...  # 添加一个或多个文件到暂存区
$ git add [dir]                # 添加指定目录到暂存区，包括其子目录
$ git add .                    # 添加当前目录下的所有文件到暂存区
```

然后，利用```git commit```命令将暂存区内容添加到本地仓库中：

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

可以先```git pull```拉取远程仓库的最新版本融合到本地，再重新上传一次代码（即重复上述操作）。更多问题，可以参考这篇博文：[Git push 时如何避免出现 "Merge branch 'master' of ..."](https://www.cnblogs.com/Sinte-Beuve/p/9195018.html).

## V. 常用命令行详解

### (X) git pull - 下载远程代码并合并
```git pull```命令用于从远程获取代码并合并本地的版本。```git pull```其实就是```git fetch```和```git merge FETCH_HEAD```的简写。

```
$ git pull <远程主机名> <远程分支名>:<本地分支名>
```

### (X) git push - 	上传远程代码并合并

```git push```命令用于从将本地的分支版本上传到远程并合并。

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
