### Windows 10 下， shift + 右击打开‘cmd 窗口’

1. 打开```注册表编辑器```，找到如下：
```
计算机\HKEY_CLASSES_ROOT\Directory\Background\shell\cmd
```
![](Windows_191029_files/1.png)

2. 将右侧的`HideBasedOnVelocityId`修改为`ShowBasedOnVelocityId`即可

![](Windows_191029_files/2.png)

3. 效果如下：

![](Windows_191029_files/3.png)

### finsh!

参考链接：
* [Win10如何把Shift+右键菜单中“在此处打开Powershell”改成命令行CMD](https://zhuanlan.zhihu.com/p/38166769)
* [Win10恢复Shift+右键菜单“在此处打开命令窗口”](https://www.cnblogs.com/mq0036/p/14656463.html)
