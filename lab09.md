---
layout: default
---

# 以洗衣机为例介绍自顶向下，逐步求精

## 名词解释：自顶向下

自顶向下（top-down）的分析算法通过在最左推导中描述出各个步骤来分析记号串输入。将大型的数字电路设计分割成大小不一的小模块来实现特定的功能，最后通过由顶层模块调用子模块来实现整体功能，这就是Top-Down的设计思想。

[参考百度百科](https://baike.baidu.com/item/%E8%87%AA%E9%A1%B6%E5%90%91%E4%B8%8B/9827072?fr=aladdin)

op-down and bottom-up are both strategies of information processing and knowledge ordering, used in a variety of fields including software, humanistic and scientific theories (see systemics), and management and organization. In practice, they can be seen as a style of thinking, teaching, or leadership. 

[参考维基百科](https://en.wikipedia.org/wiki/Top-down_and_bottom-up_design)

总之，自顶向下的思想就是将复杂的问题分割成小较容易解决的问题进行解决。

## 洗衣机的例子
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab%E6%B4%97%E8%A1%A3%E6%9C%BA.jpg)
常见的洗衣机有以下流程：浸洗、洗涤、漂洗、脱水，当我们选择不同的洗涤模式（例如快洗、标准洗、强洗等）时，系统会自动的帮我们制定好洗衣流程。我们也可以人为的去设定各个流程执行的时间以及用水的多少。

一个常见的洗衣流程伪代码如下：
1. 读取用户指令
2. 注水至水位线
3. 浸泡指定时间
4. 洗涤（电动机按一定的规律转动）
5. 排水
6. 注水至水位线
7. 漂洗（电动机按漂洗的程序转动）
8. 排水
9. 甩干（电动机高速旋转）
10. 结束并发出蜂鸣声提醒使用者

或者我们可以写成
READ instruction//including time and water limit
WHILE(water < water limit)
    get water
WHILE(time < time limit)
    do nothing//steeping
wash
WHILE(water > 0)
    drain away water
WHILE(water < water limit)
    get water
rinse
WHILE(water > 0)
    drain away water
tumble-dry
make noise
END




