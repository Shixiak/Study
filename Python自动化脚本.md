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
dlg 

#打印窗口所有的控件
dlg.print_control_identifiers()
```	
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5MjU2NDM2Nyw5OTg0OTY1MzEsOTk4ND
k2NTMxLC0xNTM0Njc3NTA3LC03NjcxODQ0MCwtMjU3NDY2MjY3
LDE3ODM1ODY4OTEsLTExODc3NjEwMDgsLTE1NTgzNDYwOTYsNT
QxNzE1Mjc0LDIyMjc4NDExOSwtMTM4MjkxMDM3MV19
-->