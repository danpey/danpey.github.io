# CentOS系统的联网配置

原装的CentOS系统是默认禁止联网的，此时需要手动配置该系统。
首先用root账户登录系统
``` bash
$ su -
```
然后输入ls查看文件开头为ifcfg-eno*的文件：
```
$ ls /etc/sysconfig/network-scripts/
```
然后使用vi进行编辑（最后的文件名为你上面搜到的文件名开头为ifcfg-eno的文件）：
```
$ vi /etc/sysconfig/network-scripts/ifcfg-eno*
```
（*号部分请自动补全）
键盘点击‘i’进入编辑模式。
然后把里面的`ONBOOT=no`改成`ONBOOT=yes`。
按键盘Esc键退出编辑模式，然后输入`:wq`保存退出。
最后重启系统即可打开联网设置。
```
$ ifconfig
```
输入`ifconfig`后查看当前IP，如果IP显示说明网络已正常连接。（IP非127.0.0.1的本地IP）

参考网址：
1. [CentOS 7怎么联网](https://jingyan.baidu.com/article/215817f78c9cde1eda14231e.html)