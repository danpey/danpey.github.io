![Git](https://git-scm.com/images/logo@2x.png)

# 1. Git 常用指令
本文介绍Git的常用指令，并不代表Git的所有功能仅限于此。仅仅为我常用的指令记录于此。
[回到导航](Git导航.md)

## 1.1. 安装 Git
Git安装平台主要有Mac OS X，Windows，Linux/Unix这几大平台。这里主要介绍Windows和Linux两大平台的安装。

### 1.1.1. Linux平台

#### 1.1.1.1. Ubuntu
``` bash
sudo apt-get install git
```

#### 1.1.1.2. CentOS
```
sudo yum install git
```

### 1.1.2. windows平台
[点此进入下载](https://git-scm.com/downloads)
下载完成后双击打开安装即可

## 1.2. 首次使用

### 1.2.1.  使用环境

#### 1.2.1.1. linux
linux用户无论是Ubuntu系统或者是CentOS系统，都是可以在终端直接使用git指令。

#### 1.2.1.2. windows
windows用户可以使用两种方式，GUI或者命令行形式。
打开Git GUI程序即可打开Git的GUI，使用界面进行操作。
打开Git Bash即可打开命令行操作，这里主要介绍命令行操作的Git。

### 1.2.2. 配置git
在首次使用之前，都需要配置Git：
``` bash
git config --global user.name [your name]
git config --global user.email [your email]
```

## 1.3. 获取仓库
我们可以直接获取一个搭建好的git仓库，比如我在码云上搭建好一个仓库，就可以直接clone下来。
```
git clone https://gitee.com/username/xxx.git  /home/username/git/
```
如果是开源的仓库，直接clone就可以获取仓库内容，如果是私有仓库，clone指令之后还需要输入用户名和密码，如果输入错误便clone失败。
如果想要切换到仓库的分支：
``` bash
git checkout [分支名]
```
查看所有分支：
``` bash
git branch -a
```

## 1.4. 提交代码（上传）
如果相比于旧版本有新的文件加入，可以使用以下指令将目录下所有文件加载到git暂存区：
``` bash
git add .
```

提交文件并备注提交信息：
```
git commit -m "first commit"
```

将本地提交的文件和信息发送到远程仓库：
```
git push origin master
```

**注意：后面的master意味着主分支，如果你已经切换到其他分支的，直接 `git push` 即可。否则可能会导致误操作提交到主分支上。**

## 1.5. 更新代码（下载）
从远程仓库更新代码到本地：
可以先查看远程仓库：
```
git remote -v
```

然后下载远程仓库的代码：
```
git fetch
```

更新文件：
```
git checkout .
```

合并文件：
```
git merge
```

`END`
最后编辑于2020.09.14