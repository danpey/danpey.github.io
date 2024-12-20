# 记录一次git自动拉取提交

首先贴一下Git自动推拉的bat指令。
``` bash
@echo off
@call :output >> F:\home\VNoteBooks\otherbooklog\otherbook_%DATE:~0,4%_%DATE:~5,2%_log.txt
echo git处理已结束，日志已保存在otherbooklog\otherbook_%DATE:~0,4%_%DATE:~5,2%_log.txt中
exit

:output
F:
echo 开始自动git处理 %date% %time%
cd F:\home\VNoteBooks\OtherBook
git pull
git add .
git commit -m Danpe_Dell_AutoCommit_%DATE:~0,4%-%DATE:~5,2%-%DATE:~8,2%_%TIME:~0,2%-%TIME:~3,2%-%TIME:~6,2%
git push
echo 自动git处理完成 %date% %time%
echo .
```
前面几句是方便用于将执行过程保存到日志中。
里面需要注意的是日志保存路径以及git仓库所在的路径，根据需要更改即可。然后就是commit提交的备注，前面可以用于备注是哪台电脑自动更新的。比如这里备注Danpe_Dell。后面备注的是日期和时间。

然后是主机启动时的bat指令：
``` bash
@echo off
if "%1" == "h" goto begin 
mshta vbscript:createobject("wscript.shell").run("%~nx0 h",0)(window.close)&&exit 
:begin
call echo 执行同步指令，执行时间%DATE:~0,4%-%DATE:~5,2%-%DATE:~8,2%_%TIME:~0,2%-%TIME:~3,2%-%TIME:~6,2% >> F:\home\VNoteBooks\shutdown_log.txt
start /B /wait F:\home\VNoteBooks\AutoUpdateOtherBook.bat >> F:\home\VNoteBooks\otherbook_log.txt
start /B /wait F:\home\VNoteBooks\AutoUpdateDanpey.bat >> F:\home\VNoteBooks\danpey_log.txt
exit
```
最前面几句用于隐藏窗口，实现后台执行。实现无感登录电脑，最后面两句才是执行相应的bat指令并保存在log日志里。
通过`win+R`键打开运行窗口，输入`shell:startup`打开用户自启动程序列表，然后将此bat文件复制快捷方式到里面即可，后续启动电脑时不会立刻启动此程序，而是在用户登录后到桌面后才会运行此程序。

主机关机时的bat指令：
``` bash
@echo off
echo 即将关机，请稍等。。。
call echo 执行关机指令，执行时间%DATE:~0,4%-%DATE:~5,2%-%DATE:~8,2%_%TIME:~0,2%-%TIME:~3,2%-%TIME:~6,2% >> F:\home\VNoteBooks\shutdown_log.txt
start /B /wait F:\home\VNoteBooks\AutoUpdateOtherBook.bat >> F:\home\VNoteBooks\otherbook_log.txt
start /B /wait F:\home\VNoteBooks\AutoUpdateDanpey.bat >> F:\home\VNoteBooks\danpey_log.txt
C:\Windows\SysWOW64\shutdown.exe -s -t 0
```

主机重启时的bat指令：
``` bash
@echo off
echo 即将重启，请稍等。。。
call echo 执行重启指令，执行时间%DATE:~0,4%-%DATE:~5,2%-%DATE:~8,2%_%TIME:~0,2%-%TIME:~3,2%-%TIME:~6,2% >> F:\home\VNoteBooks\shutdown_log.txt
start /B /wait F:\home\VNoteBooks\AutoUpdateOtherBook.bat >> F:\home\VNoteBooks\otherbook_log.txt
start /B /wait F:\home\VNoteBooks\AutoUpdateDanpey.bat >> F:\home\VNoteBooks\danpey_log.txt
C:\Windows\SysWOW64\shutdown.exe -r -t 0
```
关机和重启指令的区别主要只有最后一句的区别，以及日志和提示内容的区别。注意以上的文件路径根据自己需要修改即可。