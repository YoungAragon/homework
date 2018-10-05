---
layout: default
title: 我制作的第一个HTML5游戏经历
---

# **总括**
本文是我第一次制作HTML5游戏的大致过程，我所制作的是一个玩家通过发射子弹消灭怪物的游戏,参考了[construct guide](https://www.scirra.com/tutorials/37/beginners-guide-to-construct-2/page-1)

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

# **添加游戏对象**
在添加游戏对象之前我们必须新建一个图层，新建图层只需点击刚才锁定键旁边的加号即可。 这时候我们要开始插入对象啦，这个游戏的对象分别有玩家、怪物、子弹和爆炸。我们可以上网去搜索自己想要的造型。

插入操作类似于刚才设置背景的操作：
1、双击插入对象
2、选择sprite对象
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-6.png)
其他操作同上

重复此过程将四个对象都插入，我们可以为四个对象命名以区别，方法是在右下角 右键点击对象，选择重命名即可。注意还要添加鼠标和键盘对象，因为这个游戏需要鼠标和键盘输入，但是后二者不会再对象框里面显示出来。
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-7.png)

---

# 行为
目前为止，游戏的背景和对象是有了，但是他们都是静止不动的，这当然是不行的，所以我们要为这些对象添加行为，让他们动起来。行为是Construct 2中的预打包功能。Construct 2有这些行为;

>8方向运动。这使您可以使用箭头键移动对象。它会很好地适应玩家的运动。
>子弹运动。这只是以当前角度向前移动一个物体。它对玩家的子弹很有用。尽管有这个名字，它也可以很好地移动怪物 - 因为所有的移动都是以某种速度向前移动物体。
>滚动到。这使得屏幕在移动时跟随对象（也称为滚动）。这对玩家有用。
>绑定到布局。这将停止一个物体离开布局区域。这对玩家也很有用，所以他们不能在游戏区域外游荡！
>破坏外部布局。一个离开布局区域的对象，如果它停止，则会破坏它。它对我们的子弹很有用。没有它，子弹将永远飞离屏幕，总是占用一点内存和处理能力。相反，我们应该在他们离开布局后销毁子弹。
>淡出。这逐渐使物体淡出，我们将用于爆炸。

让我们将这些行为添加到需要它们的对象中，具体操作如下：
首先为玩家添加8方向移动，我们要先在右下角的项目中选中玩家，并在左边的属性栏里面找到“Behaviors”，并进行以下操作：
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-8.png)

再次执行相同操作，这次添加Scroll To行为，使屏幕跟随播放器，以Bound to layout 行为，以使它们保持在布局中。操作完得到如下结果：
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-9.png)

同样的我们为其他对象添加行为：
子弹：添加 Bullet movement 和 Destroy outside layout行为
怪物：添加 Bullet movement行为
爆炸：添加 Fade行为

现在你可以试着点击窗口左上方的运行（run layout）按钮运行游戏，你会发现怪兽和子弹具有相同的移动速度，我们要对其进行“限速”。
我们选中怪物对象，在属性栏里面有speed这一项目，将参数400修改为80，同样的我也可以采用相同的办法提高子弹的射速。
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-10.png)

---

# **事件**
我们还要通过定义一些事件来使游戏运行，最简单的当子弹与怪物相撞时消灭怪物等等。首先我们得找到事件表1
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab2-11.png)

我们想让玩家总是看着鼠标。因此如果我们让每个刻度线都让玩家面向鼠标，它们将始终面向鼠标。具体操作如下