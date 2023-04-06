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
dlg = app["]

#打印窗口所有的控件
dlg.print_control_identifiers()
```	
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDkwMjY0MDMsOTk4NDk2NTMxLDk5OD
Q5NjUzMSwtMTUzNDY3NzUwNywtNzY3MTg0NDAsLTI1NzQ2NjI2
NywxNzgzNTg2ODkxLC0xMTg3NzYxMDA4LC0xNTU4MzQ2MDk2LD
U0MTcxNTI3NCwyMjI3ODQxMTksLTEzODI5MTAzNzFdfQ==
-->