---
layout: default
title: 我制作的第一个HTML5游戏经历
---

# **总括**
本文是我第一次制作HTML5游戏的大致过程，我所制作的是一个玩家通过发射子弹消灭怪物的游戏

---

# **安装Construct 2**
Construct 2编辑器仅适用于Windows，我们能够使用Construct 2创造任何类型的2D游戏，所制作的游戏可以在任何地方运行，例如Mac，Linux或iPad。

---

# **背景的设置和锁定**
首先在窗口左上角找到“文件”选项，点击并选择创建新的空项目。
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-1.png)

这时屏幕上中央会产生一个空白的页面，双击该页面以添加背景，并选择“Tiled Background”选项。
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-2.png)

在选择插入后，鼠标的指针会变成十字形，此时只需在空白页上点击，便会跳出图片编辑框，点击上方第二个选项载入图片。
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-3.png)

点击关闭后可以看到你所选择的背景已经在页面上了，我通过手动拉取图片使其覆盖视图（ps：可通过ctrl+鼠标滚轮可以缩小或放大视图）。现在我们要添加更多对象。但是，我们会不小心选择平铺的背景，除非我们锁定它，使其无法选择。我们使用分层系统来做到这一点。现在我们把视角转换到窗口右上方选取layers.
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-4.png)

并将其锁定
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-5.png)

这样一来背景就被我们锁定无法选取了，当想要编辑或者更换背景时，在点击锁定按钮即可解锁。为了区别还可以将图层名字命名为background，点击右键点击重命名即可实现此操作。

---

# **添加游戏对象
在添加游戏对象之前我们必须新建一个图层，新建图层只需点击刚才锁定键旁边的加号即可。 这时候我们要开始插入对象啦，这个游戏的对象分别有玩家、怪物、子弹和爆炸。我们可以上网去搜索自己想要的造型。

插入操作类似于刚才设置背景的操作：
1、双击插入对象
2、选择sprite对象
![]()
其他操作同上

重复此过程将四个对象都插入，我们可以为四个对象命名以区别，方法是在右下角 右键点击对象，选择重命名即可。
![]()
