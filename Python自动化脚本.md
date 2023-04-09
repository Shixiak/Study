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
#窗口最大化
dlg.maximize()

#窗口最小化
dlg.minimize()

#窗口恢复正常
dlg.restore()

#获得窗口显示状态：最大化(1)，正常(0)
status = dlg.get_show_state()

#关闭窗口
dlg.close()

#获取窗口显示位置
rect = dlg.rectangle
rect = (L,T,R,B)
```

## P9 窗口控件的选择
```Python
#查看窗口的方法

#方法一：
#使用viewWizard查看

#方法二
#打印窗口所有的控件
dlg.print_control_identifiers()

#要素过多建议不会就直接看视频
```

## P10 窗口控件的分类
```Python
#一个区域是一个窗口，窗口上有不同的控件
```

## P11 控件相关属性的获取
```Python
#选择菜单
menu = dlg["menu"]

#选择菜单项：文件
File = menu.child_window(title = "文件")

#查看控件类型
print(dlg.wrapper_object())
print(menu.wrapper_object())
print(File.wrapper_object())

#查看控件支持的方法
print(dir(dlg.wrapper_object()))

#控件文本内容的获取
print(File.texts())

#获取控件子元素
print(dlg.children())

#获取菜单子元素
print(menu.children())

#获取控件的类名
print(menu.class_name())

#获取控件的所有的属性，返回的是字典
print(menu.get_properties())
```

## P12 控件及窗口的截图操作
```Python
menu = dlg["menu"]
File = menu.child_window(title = "文件")

#截图处理
Pic = dlg.caputure_as_image
Pic.
#截图窗口
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwNDg3ODY4MDksLTE1MjgxMTgzMTgsMT
gzNzgwNzA2MSwtMjAzNzAxNzgyMSwxMzg0NzgyNTIzLC0xODY0
NTUwODgxLDk5ODQ5NjUzMSw5OTg0OTY1MzEsLTE1MzQ2Nzc1MD
csLTc2NzE4NDQwLC0yNTc0NjYyNjcsMTc4MzU4Njg5MSwtMTE4
Nzc2MTAwOCwtMTU1ODM0NjA5Niw1NDE3MTUyNzQsMjIyNzg0MT
E5LC0xMzgyOTEwMzcxXX0=
-->