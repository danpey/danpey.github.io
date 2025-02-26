# Debian安装Jellyfin媒体服务器

主要参考网页：[如何在 Ubuntu 24.04、22.04 或 20.04 上安装 Jellyfin 媒体服务器](https://blog.csdn.net/csdn_life18/article/details/142666458)

安装前，首先更新一下软件包的库

``` bash
sudo apt-get update && sudo apt upgrade
```

安装Jellyfin媒体服务器的初始软件包

``` bash
sudo apt-get install apt-transport-https ca-certificates curl -y
```

导入Jellyfin GPG密钥

``` bash
curl -fsSL https://repo.jellyfin.org/ubuntu/jellyfin_team.gpg.key | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/jellyfin.gpg > /dev/null
```

导入Jellyfin存储库

``` bash
echo "deb [arch=$( dpkg --print-architecture )] https://repo.jellyfin.org/$( awk -F'=' '/^ID=/{ print $NF }' /etc/os-release ) $( awk -F'=' '/^VERSION_CODENAME=/{ print $NF }' /etc/os-release ) main" | sudo tee /etc/apt/sources.list.d/jellyfin.list
```

再次更新软件包
``` bash
sudo apt-get update
```

开始安装Jellyfin
``` bash
sudo apt-get install jellyfin
```
安装过程比较漫长，网速好的时候不需要翻墙就能完成下载。
完成安装后，Jellyfin会自动启动，为了确认，可以使用以下命令检查Jellyfin的状态。
``` bash
systemctl status jellyfin
```
如果没有启动，则可以使用以下命令启动jellyfin
``` bash
sudo systemctl start jellyfin
```

配置系统启动时，自动启动jellyfin
``` bash
sudo systemctl enable jellyfin
```

如果出现中文乱码，可以将系统字体更换为以下路径的字体：[DejaVuSans中文字体](https://wwbf.lanzouw.com/iToXe2babwwj)
被替换的字体路径为：`/usr/share/fonts/truetype/dejavu/`

Jellyfin Web UI的默认端口为8096，可以访问`http://127.0.0.1:8096`来进入UI管理页面。
进入后，可以配置语言等设置，添加媒体库等内容。
至此，Jellyfin安装完成。
