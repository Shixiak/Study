# 进度
* P3-自动化的切入点
* P4-程序检查辅助工具的使用
* P5-pywinauto打开指定应用程序
* P6-pywinauto连接已经打开的程序
* P7-pywinauto选择指定的窗口
	* 通过类名和窗口名称选择窗口
	* app.connect.
* P8-窗口的操作方法
	* 最大化和最小化的操作

* P9-窗口控件的选择

## P7 选择指定的窗口
```Python
#方式一
#使用窗口类名选择窗口
dlg = app["TNavicatMainForm"]
#通过窗口标题选择
dlg = app["Navicat for MySQL“]

#方式二
#app.窗口类名
dlg = app.TNavicatMainForm
#app.窗口标题
dlg = app.Navicat for MySQL
#这条语句显然出问题了，因此实际使用中一般推荐使用方式一

#打印窗口所有的控件
dlg.print_control_identifiers()
```	

## P8 窗口的操作方法
```Python
# 
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAxNzg0MTQwMSwtMTg2NDU1MDg4MSw5OT
g0OTY1MzEsOTk4NDk2NTMxLC0xNTM0Njc3NTA3LC03NjcxODQ0
MCwtMjU3NDY2MjY3LDE3ODM1ODY4OTEsLTExODc3NjEwMDgsLT
E1NTgzNDYwOTYsNTQxNzE1Mjc0LDIyMjc4NDExOSwtMTM4Mjkx
MDM3MV19
-->