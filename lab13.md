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
	
int snakeX[SNAKE_MAX_LENGTH] = {5,4,3,2,1};//第一个元素对应蛇头 
int snakeY[SNAKE_MAX_LENGTH] = {1,1,1,1,1};//蛇身子和蛇头坐标 
int snakeLength = 5;//初始长度
int foodX;
int foodY;

```

* 这里补充一个打印图案的函数：
```c
void output ()//打印图像的函数 
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
	output();
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
	output();
	}
}//自然后来功能多了后头部也会有相应改动！！
```

* snakeMove函数

分析：在考虑蛇身不变长的情况下，每一次移动则只需对蛇头坐标进行变换，蛇身坐标覆盖前一个蛇身（蛇头）的坐标，原来最后一个坐标的位置则使用空格代替。从而绘制出新的一张图案再次打印。具体代码如下：
```c
void snakeMove(int x,int y){
	map[snakeY[snakeLength-1]][snakeX[snakeLength-1]] = ' ';
	for(int i = snakeLength - 1; i > 0; i --) {								 
		snakeX[i] = snakeX[i - 1];		
		snakeY[i] = snakeY[i - 1];
		map[snakeY[i]][snakeX[i]] = 'X';
	}
	snakeX[0] += x;
	snakeY[0] += y;
	map[snakeY[0]][snakeX[0]] = 'H';
}
```
从而完成任务一，效果如下：
![](https://github.com/YoungAragon/swi-homework/blob/gh-pages/images/lab13/%E8%B4%AA%E5%90%83%E8%9B%871.gif)

---

### 任务2：会吃的蛇
功能要求：
1. snake 头撞到身体、障碍（边界或你在地图中定义） 游戏结束

分析：游戏结束有以下标准：一是蛇碰到墙壁（可以通过蛇头坐标与墙壁坐标重合来实现）。二是碰到身体（可以通过蛇头坐标和蛇身坐标重合来实现）。当满足二者之一的条件时结束主函数中的循环。

C语言实现：
```c
int gameover(void){
	if(snakeX[0] == 0||snakeX[0] == 12||snakeY[0] == 0||snakeY[0] == 12)	//碰到框架游戏结束 
		return 0;

	for(int i=1;i<snakeLength;i++) {
		if(snakeX[0] == snakeX[i]&&snakeY[0]==snakeY[i])	//头碰到自己游戏结束 
				return 0;
	}
	return 1;
}
```


2. snake 头吃到食物，snake就长一节

分析：这包含了两个函数，一个是放置食物，一个是蛇身边长。

首先是放置食物的函数：这里用了rand这个库函数。
```c
void put_money (void) {
	//随机设置食物位置 
	foodX = rand () % 11;
	foodY = rand ()  % 11;//食物的坐标已经被设置为外部变量。
	if (map[foodY][foodX] == ' ') {//判断位置是否为空 
		map[foodY][foodX]=SNAKE_FOOD;
	}
	else	//不为空重新调用 
		put_money ();		
}
```
蛇身伸长：
```c
void snakeExtent (void) {
	put_money ();//蛇吃到食物后重置食物位置
	if (snakeLength < SNAKE_MAX_LENGTH) { //小于最长长度 
		snakeY[snakeLength] = snakeY[snakeLength-1];
		snakeX[snakeLength] = snakeX[snakeLength-1];
		snakeLength ++ ;
	} 
	else 
		map[snakeY[snakeLength-1]][snakeX[snakeLength-1]] = ' '; //大于最长长度 
}
```
任务二完成！

---

# 小结
本次实验学到了很多新东西，比如如何刷新屏幕，如何使用随机数。特别感谢以下博客对我的帮助
(https://blog.csdn.net/qq_40135006/article/details/78904825)
(https://blog.csdn.net/zhangweikun1998/article/details/78901988)

好多思想都是从文章中学到的
最后附上一张总代码
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
int gameover(void);
void snakeExtent (void);

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
	
int snakeX[SNAKE_MAX_LENGTH] = {5,4,3,2,1};//第一个元素对应蛇头 
int snakeY[SNAKE_MAX_LENGTH] = {1,1,1,1,1};//蛇身子和蛇头坐标 
int snakeLength = 5;//初始长度
int foodX;
int foodY;

/****************************************************************/ //预处理

void output ()//打印图像的函数 
{
    int i=0;
    system("cls");//system(“cls”); 指令不断的清空屏幕上的内容，接下来的指令再进行反复地填充。
    for ( i=0; i<12; i++ ) {
        printf("%s\n", map[i]);
    }
}

int main(){
	put_money();
	output();
	char c;
	while(gameover()){
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
	output();
	}
	return 0;
}

void snakeMove(int x,int y){
	int i; 
	if(snakeX[0] + x == foodX && snakeY[0] + y == foodY) 				//判断是否吃到食物 ,如是便使蛇伸长 
		snakeExtent() ;						
	else 
		map[snakeY[snakeLength - 1]][snakeX[snakeLength - 1]] = ' ';	//如果没有吃到食物,把蛇的最后一段删除 
	for(int i = snakeLength - 1; i > 0; i --) {								 
		snakeX[i] = snakeX[i - 1];		
		snakeY[i] = snakeY[i - 1];
		map[snakeY[i]][snakeX[i]] = SNAKE_BODY;
	}
	snakeX[0] += x;
	snakeY[0] += y;
	map[snakeY[0]][snakeX[0]] = SNAKE_HEAD;
}

int gameover(void){
	if(snakeX[0] == 0||snakeX[0] == 12||snakeY[0] == 0||snakeY[0] == 12)	//碰到框架游戏结束 
		return 0;

	for(int i=1;i<snakeLength;i++) {
		if(snakeX[0] == snakeX[i]&&snakeY[0]==snakeY[i])	//头碰到自己游戏结束 
				return 0;
	}
	return 1;
}

void put_money (void) {
	//随机设置食物位置 
	foodX = rand () % 11;
	foodY = rand ()  % 11;
	//判断位置是否为空 
	if (map[foodY][foodX] == ' ') {
		map[foodY][foodX]=SNAKE_FOOD;
	}
	else	//不为空重新调用 
		put_money ();		
}

void snakeExtent (void) {
	put_money ();//蛇吃到食物后重置食物位置
	if (snakeLength < SNAKE_MAX_LENGTH) { //小于最长长度 
		snakeY[snakeLength] = snakeY[snakeLength-1];
		snakeX[snakeLength] = snakeX[snakeLength-1];
		snakeLength ++ ;
	} 
	else 
		map[snakeY[snakeLength-1]][snakeX[snakeLength-1]] = ' '; //大于最长长度 
}
```
