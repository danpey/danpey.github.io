# 小乌龟TortoiseGit解决图标问题

检查注册表（regedit）：
路径：HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers

查看该路径下的小乌龟文件前面是否有足够多的空格，然后重命名（前面增加空格）令其在所有项的最前方。
然后通过任务栏重启Windows资源管理器即可