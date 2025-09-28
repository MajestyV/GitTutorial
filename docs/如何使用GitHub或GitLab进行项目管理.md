# 如何使用GitHub或GitLab进行项目管理

## I. 简介

[GitHub](https://github.com/)和[GitLab](https://about.gitlab.com/)都是目前全球流行的代码托管平台，主要用于软件开发和版本控制。它基于 Git 版本控制系统，允许开发者在云端托管、管理和协作开发项目。通过 GitHub，用户可以方便地提交代码、跟踪问题、进行代码审核以及管理项目文档。平台支持分支管理、Pull Request、Issue 等功能，极大地促进了开源项目和团队协作的效率。除了代码托管，GitHub 还提供了丰富的社区资源，开发者可以参与开源项目、学习技术知识，并与全球的技术爱好者交流互动。

## II. 环境配置

GitHub和GitLab的使用方式是类似的，因此在此教程中，我们以GitHub为例进行详细地介绍。在用户熟悉了GitHub的使用之后，运用GitLab进行项目代码的维护将是信手拈来之事。

为了方便利用GitHub进行项目管理，我们可以先建立PC与对应GitHub账户之间的连接。由于本地Git仓库和GitHub远程仓库之间的传输是通过SSH加密的，所以我们需要配置验证信息。首先，我们可以使用以下命令在本地生成SSH Key：

```shell
$ ssh-keygen -t rsa -C "youremail@example.com"
```

有时我们的本地机器可能会用到多个Git账号对于不同的项目或者是远程服务器，此时我们就需要不同的SSH Key来对应不同Git账号。但是如果我们已经有生成好的SSH Key文件又直接通过上述命令行来生成新Key，新的密钥就会把老的密钥覆盖掉。此时，我们就可以通过给密钥文件定义新的文件名加以区分：

```shell
$ ssh-keygen -t rsa -C "youremail@example.com" -f ~/.ssh/id_rsa_github
```

标签```-f```指定密钥文件存储文件名，利用```-f```标签，我们可以给密钥文件赋予新的文件名。关于一台本地终端如何配置多个SSH Key，更多细节可以参考这篇博文：[Mac上配置SSH - 多个SSH](https://www.jianshu.com/p/d29ef6aefee2)。标签```-t```指定密钥类型，默认是 rsa ，可以省略。标签```-C```后面的内容为注释，为了方便区分，可以把```your_email@youremail.com```改为个人的GitHub账号（当然，不管也是没问题的）。之后会要求确认路径和输入密码，在此只需一直回车选择默认选项就行，就像这样：

```shell
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

成功的话会在```~/```下生成```.ssh```文件夹，里面存放着私钥```id_rsa```和公钥```id_rsa.pub```。 利用记事本打开```id_rsa.pub```，复制里面的公钥并上传到GitHub即可。详细操作可见这篇博文：[如何使用SSH连接到Github](https://zhuanlan.zhihu.com/p/111344840)。接下来，我们还需激活与GitHub的连接，要完成这一步，只需在本地终端执行以下命令即可：

```
$ ssh -T git@github.com
Hi MajestyV! You've successfully authenticated, but GitHub does not provide shell access.
```

有时新的客户端初次连接GitHub时会显示这种警报：

```shell
$ ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ECDSA key fingerprint is SHA256:XXXXXXXXXXXXXXXXXX.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

这种情况下其实没有任何问题，就是应当注意不要直接回车（按```enter```)，要先输入```yes```再```enter```：

```shell
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ECDSA key fingerprint is SHA256:XXXXXXXXXXXXXXXXXX.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com,20.205.243.166' (ECDSA) to the list of known hosts.
Hi MajestyV! You've successfully authenticated, but GitHub does not provide shell access.
```

详情可以参考：[git使用--解决The authenticity of host ‘github.com (20.205.243.166)‘ can‘t be established](https://blog.csdn.net/mj_zm/article/details/120413479)。这类警报的原因是当前客户端为没有host关于GitHub网站的内容，所以出现问题。



## 疑难杂症

### a. 如何测试与GitHub的链接

经常，暗黑圣堂武士们虽然剪了辫子，但是在连接Aiur（划掉）GitHub时都会少许受阻，这里我们可以用以下的命令行测试与Aiur的链接情况：

```shell
$ ping github.com
```

