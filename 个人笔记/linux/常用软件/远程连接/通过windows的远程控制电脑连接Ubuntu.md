# 通过windows的远程控制电脑连接Ubuntu
[回到远程连接导航](远程连接导航.md)

## 前言
在局域网的远程控制中，很多诸如TeamViewer和VNC有连接不稳定和需要显示器才可以工作等问题。因此需要一个连接稳定，远程被控端可以不接显示屏。最终找到了如此方法，通过Windows自带的远程控制，易于使用，便于控制。

## 安装步骤

### 参考环境
- 控制端：Windows 10专业版 1909
- 被控端：Ubuntu 18.04

### 连接前提
**两台机器能够保证互相ping通**
- 如果Windows不能ping通Ubuntu，请检查Ubuntu防火墙设置
- 如果Ubuntu不能ping通Windows，需要开启Windows共享

### 安装xrdp
- 进入 [C-Nergy](http://www.c-nergy.be/products.html) 官网，下载xrdp脚本：
![C-Nergy官网](https://vnotebook-1258832516.cos.ap-shanghai.myqcloud.com/1600140469_20200915103129120_16120.png)
可以右键复制链接地址，然后在你的Ubuntu终端直接用wget下载：
``` bash
wget http://c-nergy.be/downloads/xRDP/xrdp-installer-1.2.zip
```

- 点击 [How to](https://c-nergy.be/blog/?p=14888)，具体参考官网给出的安装步骤。我这里采用标准安装，依次执行以下步骤即可：

``` bash
# 解压缩
unzip xrdp-installer-1.2.zip
# 修改权限
chmod +x ~/Downloads/xrdp-installer-1.2.sh
# 运行脚本
./xrdp-installer-1.2.sh
```
**注意：**
- **最后的运行脚本请勿使用管理员模式进行操作！无论是sudo还是root都不可以，如果是管理员模式，程序会自行退出，请使用普通账号进行操作！**
- **如果需要传输声音的，请参考官网的指南进行操作！标准安装没有传输声音。**
安装完成后，请检查Ubuntu是否已经设置为开机自动登录用户，如是，需要关闭开机自动登录用户。
打开设置->详细信息->用户，关闭自动登录：
![关闭自动登录](https://vnotebook-1258832516.cos.ap-shanghai.myqcloud.com/1600140470_20200915110742534_11511.png)

## 远程连接
最后，打开Windows远程桌面，输入Ubuntu的主机IP地址，然后点击左下角的显示选项，点击上方的本地资源：
![远程桌面本地资源](https://vnotebook-1258832516.cos.ap-shanghai.myqcloud.com/1600140470_20200915111220866_1653.png)
如图所示，这里可以配置一些本地资源相关的设置，我们把本地设备和资源内的剪贴板勾上，然后点开详细信息：
![远程连接本地设备和资源详细信息](https://vnotebook-1258832516.cos.ap-shanghai.myqcloud.com/1600140470_20200915111330730_2554.png)

在详细信息中将视频捕获设备勾选上即可。然后点击确定。
回到远程桌面连接的常规页面，我们可以输入用户名，也就是之前你在Ubuntu上登录的用户名，然后点击连接，输入用户密码即可使用。

## 更换桌面风格

如果在使用中发现一些兼容性问题，可以考虑使用xfce桌面。
安装也非常简单，就是风格会不太适应：
``` bash
# 安装xfce4
sudo apt-get install xfce4
# 配置文件
cd ~
echo xfce4-session > ./.xsession
# 重启xrdp服务
sudo service xrdp restart
```

END
最后编辑于2020.9.15
