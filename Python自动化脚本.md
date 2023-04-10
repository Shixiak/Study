# 进度

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

#截图窗口
Pic = dlg.caputure_as_image
Pic.save("01.png")
```

## P13 菜单控件相关的操作
```Python
#获取菜单的子菜单项
print(menu.item())

#通过下标选择菜单项
m = menu.item_by_index(0)
print(m)

#通过路径选择菜单项
File = menu.item_by_path("文件")
new_connect = menu.item_by_path("文件->新建连接...")


#菜单项的操作方法

#获取子菜单项
File.items()
#点击的方法
File.click_input()
```

## P14 pywinauto中的等待机制
### wait方法
作用：等待窗口处于某个状态
* wait_for：等待的状态
	* exist：表示该窗口是否有效的句柄
	* visible：表示该窗口是否隐藏
	* enabled：表示该窗口是否启用
	* ready：表示该窗口是否启用并可见
	* active：表示该窗口处于活动状态
* timeout：超时时间
* retry_interval：重试间隔
```Python
new_dlg = app["新建连接"]
new.dlg.wait(wait_for("ready"), timeout = 10, retry_interval = 1)

```
这里的新建连接和上一集的新建连接...不是同一个东西，一个是控件，一个是窗口名
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMzMTIzOTUwNSwxMTg2ODIxNjA1LC0xNz
I0NjgxMDQ3LDE5MjQxNzQ1MjYsLTE1MjgxMTgzMTgsMTgzNzgw
NzA2MSwtMjAzNzAxNzgyMSwxMzg0NzgyNTIzLC0xODY0NTUwOD
gxLDk5ODQ5NjUzMSw5OTg0OTY1MzEsLTE1MzQ2Nzc1MDcsLTc2
NzE4NDQwLC0yNTc0NjYyNjcsMTc4MzU4Njg5MSwtMTE4Nzc2MT
AwOCwtMTU1ODM0NjA5Niw1NDE3MTUyNzQsMjIyNzg0MTE5LC0x
MzgyOTEwMzcxXX0=
-->