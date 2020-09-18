![Git](https://git-scm.com/images/logo@2x.png)

# Git服务器搭建
本教程仅适用于Linux系统，Ubuntu或者CentOS皆可。
[回到导航](Git导航.md)

**以下皆以Ubuntu 18.04 为参考环境**

## 安装Git
- 如果是Ubuntu系统可用apt进行安装
- 如果是CentOS系统可用yum进行安装

``` bash
# 首先更新源
sudo apt-get update
# 然后安装相关软件和git
sudo apt-get install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel
sudo apt-get install git
```

## 创建证书登录

首先我们先创建一个git用户组和git用户，用来运行git服务：
``` bash
# 创建用户组
groupadd git
# 创建用户
useradd git -g git
```

收集所有需要登录的用户的公钥，公钥位于id_rsa.pub文件中，把我们的公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。
如果没有该文件则创建一个：

``` bash
cd /home/git/
sudo mkdir .ssh
chmod 755 .ssh
touch .ssh/authorized_keys
chmod 644 .ssh/authorized_keys
```

如果说只想你自己使用，没有其他用户的话，你也可以直接设置git的密码，然后后续也可以直接通过git来登录。
``` bash
# 开始设置密码
sudo passwd git
# 进入设置密码阶段，密码不可见
```

## 初始化Git仓库

首先选定一个目录作为Git仓库，以runoob.git为例开始初始化仓库：

``` bash
# 新建所有仓库的根地址
cd /home
sudo mkdir gitrepo
sudo chown git:git gitrepo/
cd gitrepo
# 创建runoob.git仓库
sudo git init --bare runoob.git
sudo chown -R git:git runoob.git
```

## 克隆仓库
在其他电脑，可以使用以下代码克隆仓库
``` bash
git clone git@192.168.1.50:/home/gitrepo/runoob.git
```
192.168.1.50为Git服务器IP，需要将其修改为你自己的IP。

如果你已有文件，想关联并上传到git仓库，可以按以下步骤操作：
``` bash
# 首先进入到你要上传的文件夹下
# 然后初始化git
git init
# 添加文件
git add .
# 提交并备注信息
git commit -m "first commit"
# 增加远程地址，远程地址命名为origin
git remote add origin ssh://git@192.168.1.50:/home/gitrepo/runoob.git
# 提交代码
git push origin master

# 如果远程地址增加错了，可以按以下方式进行删除：
git remote remove origin
# 增加远程地址后，可以按以下方式查看远程地址：
git remote -v
```
