---
layout: default
---

# programing1:Add 2 number
questions and answers1:

    1、PC，IR 寄存器的作用。
    2、ACC 寄存器的全称与作用。
    3、用“LOD #3”指令的执行过程，解释Fetch-Execute周期。
    4、用“ADD W” 指令的执行过程，解释Fetch-Execute周期。
    5、“LOD #3” 与 “ADD W” 指令的执行在Fetch-Execute周期级别，有什么不同。

1、

（1）PC的作用：用于读取指令

（2）IR的作用：用于存放当前正在运行的指令

2、 ACC的全称是累加器，作用是用来存放操作数和运算结果。

3、“LOD #3”指令的执行过程：PC先从内存中读取该条指令（Fetch instruction），读取的指令被传送至IR
，IR讲读取的指令分别传去Decode（Decode instruction）和MUX，MUX根据指令获取数值3（Get data），再将其传送至ALU（Execute the instruction）。

4、“ADD W” 指令的执行过程：PC先从内存中读取该条指令（Fetch instruction），读取的指令被传送至IR
，IR讲读取的指令分别传去Decode（Decode instruction），MUX根据指令到内存的W地址里获取之前存储的数据（Get data），再将其传送到ALU执行加法操作（Execute the instruction）。

5、“LOD #3” 是直接获取数据，而“ADD W” 要去内存对应的地址中提取数据。

questions and answers2：

    1、写出指令 “LOD #7” 的二进制形式，按指令结构，解释每部分的含义。
    2、解释 RAM 的地址。
    3、该机器CPU是几位的？（按累加器的位数）
    4、写出该程序对应的 C语言表达。

1、00010100 00000111
分析:第一个字节，前四位0001表示是直接获取操作数，0100代表的是LOD指令。第二个字节对应数值7，即本次获取的操作数。

2、RAM的地址对应红色阴影部分：每一个地址存放一条指令或者数据。
![]()