---
layout: default
title: 贪吃蛇实验报告
---

# 贪吃蛇实验报告

## 游戏简介
贪吃蛇游戏是一款经典的益智游戏，有PC和手机等多平台版本。既简单又耐玩。该游戏通过控制蛇头方向吃蛋，从而使得蛇变得越来越长。[百度百科](https://baike.baidu.com/item/%E8%B4%AA%E5%90%83%E8%9B%87/9510203)

## 实验目的
1. 了解字符游戏的表示
2. 体验自顶向下的设计方法实现问题求解
3. 使用伪代码表示算法
4. 使用函数抽象过程

### 任务一：会动的蛇
* 程序头部
```c
//字符版贪吃蛇
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SNAKE_MAX_LENGTH 20
#define SNAKE_HEAD 'H'
#define SNAKE_BODY 'X'
#define BLANK_CELL ' '
#define SNAKE_FOOD '$'
#define WALL_CELL '*'


//snake stepping:dy = -1(up),+1(down);dx = -1(left),+1(right) 
void snakeMove(int,int);
void put_money(void);
void output(void);
void gameover(void);

char map[12][13] = 
	{"************",
	"*XXXXH     *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"*          *",
	"************"};//地图 
	
int snakeX[SNAKE_MAX_LENGTH] = {1,2,3,4,5};//第一个元素对应蛇头 
int snakeY[SNAKE_MAX_LENGTH] = {1,1,1,1,1};//蛇身子和蛇头坐标 
int snakeLength = 5;//初始长度

```

* 这里补充一个打印图案的函数：
```c
void PrintMap ()//打印图像的函数 
{
    int i=0;
    system("cls");//system(“cls”); 指令不断的清空屏幕上的内容，接下来的指令再进行反复地填充。
    for ( i=0; i<12; i++ ) {
        printf("%s\n", map[i]);
    }
}
```
正如注释所写：通过system(“cls”)指令实现对屏幕的不断刷新。

* 主函数结构
>输出字符矩阵
	
    WHILE not 游戏结束 DO
		ch＝等待输入
		CASE ch DO
		‘A’:左前进一步，break 
		‘D’:右前进一步，break    
		‘W’:上前进一步，break    
		‘S’:下前进一步，break    
		END CASE
		输出字符矩阵
	END WHILE
	输出 Game Over!!! 

对应的c语言代码如下：
```c
int main(){
	PrintMap();
	char c;
	while(1){
		c = getchar();
		switch(c) {
			case 'A': 
				snakeMove (-1, 0);
				break;
			case 'S':
				snakeMove (0, 1);
				break;
			case 'D':
				snakeMove (1, 0);
				break; 
			case 'W':
				snakeMove (0, -1);
				break;
		}
	PrintMap();
	}
}
```

* snakeMove函数

分析：在考虑蛇身不变长的情况下，每一次移动则只需对蛇头坐标进行变换，蛇身坐标覆盖前一个蛇身（蛇头）的坐标，原来最后一个坐标的位置则使用空格代替。从而绘制出新的一张图案再次打印。具体代码如下：
```c
void snakeMove(int x,int y){
	map[snakeY[0]][snakeX[0]] = ' ';
	for(int i = 0; i < snakeLength-1; i++) {								 
		snakeX[i] = snakeX[i + 1];		
		snakeY[i] = snakeY[i + 1];
		map[snakeY[i]][snakeX[i]] = 'X';
	}
	snakeX[snakeLength-1] += x;
	snakeY[snakeLength-1] += y;
	map[snakeY[snakeLength-1]][snakeX[snakeLength-1]] = 'H';
}
```
从而完成任务一，效果如下：
![](https://github.com/YoungAragon/swi-homework/blob/gh-pages/images/lab13/%E8%B4%AA%E5%90%83%E8%9B%871.gif)

