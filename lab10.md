---
layout: default
---

# 我的python之旅
## 用python解决两道高等数学问题
运行环境
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab10-1.png)
python提供了丰富的数学函数
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab10-2.png)


---

我们今天用Python来解决两道高数问题
1. ![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/%E9%AB%98%E6%95%B01.jpg)
这是一个很经典的极限，我们来看看解答
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab10-3.png)
我们发现系统提示我们没有定义sin，所以还要添加一步用于添加基本符号的操作
```python
>>>from sympy import *
```
然后我们再来求极限
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab10-4.png)
我们发现直接有一个叫limit的函数用于求解极限，实在是太方便了！！由于c语言的缘故我开始还使用printf，发现Python的输出直接是print，更贴近实际交流

---

2.![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/%E9%AB%98%E6%95%B02.jpg)

这是又一个经典的极限，我们看看解答

![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab10-5.png)

值得注意的是，无穷在Python中是用两个英文的小写字母oo来表示的。

---

## 用python解决两道线性代数问题问题
1.![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/%E7%BA%BF%E4%BB%A32.jpg)
这是一道求解行列式的问题，我们看一下解答：
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab10-6.png)
值得注意的是，在解决矩阵问题时，我们又调用了另外的库。


---

2. ![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/%E7%BA%BF%E4%BB%A31.jpg)

这是课本上一道求A矩阵逆矩阵的问题，我们来看一下如何操作：
![](https://raw.githubusercontent.com/YoungAragon/swi-homework/gh-pages/images/lab10-7.png)

inv是一个求逆的函数。

---

# 小结
Python是一个包含很多库函数的语言，可以用来解决很多数学问题。下次还可以尝试下利用它解决泰勒展开求积分等数学问题。