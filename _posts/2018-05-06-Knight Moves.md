---
layout:     post
title:      Knight Moves
subtitle:  Knight Moves（BFS）
date:       2018-05-06
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - hdu
    - bfs
---
[http://acm.hdu.edu.cn/showproblem.php?pid=1372](http://acm.hdu.edu.cn/showproblem.php?pid=1372)
# 问题描述：
A friend of you is doing research on the Traveling Knight Problem (TKP) where you are to find the shortest closed tour of knight moves that visits each square of a given set of n squares on a chessboard exactly once. He thinks that the most difficult part of the problem is determining the smallest number of knight moves between two given squares and that, once you have accomplished this, finding the tour would be easy.
Of course you know that it is vice versa. So you offer him to write a program that solves the "difficult" part. 

Your job is to write a program that takes two squares a and b as input and then determines the number of knight moves on a shortest route from a to b. 

# 问题分析：
>给出起点a和终点b，跳日，求从a到b的需要跳的最短次数。使用BFS进行最短路搜索。

# AC代码：

```c++

#include<iostream>
#include<cmath>
using namespace std;
#include<iomanip>
#include<cstring>
#include<queue>
 
int xa,xb,ya,yb;
 
struct node{
	int x;
	int y;
	int t;
}first,nextp;
 
char a[3],b[3];
int map[10][10];
//跳日的方向 
int dir[8][2] = {-2,1,-2,-1,2,1,2,-1,-1,2,-1,-2,1,2,1,-2};
 
void bfs(){
	int i;
	queue<node>q;
	first.x = xa;
	first.y = ya;
	first.t = 0;
	map[first.x][first.y] = 1;
	q.push(first);
	while(!q.empty()){
		//去除最前的节点 
		first = q.front();
		q.pop();
		if(first.x == xb && first.y == yb){
			cout<<"To get from "<<a<<" to "<<b<<" takes "<<first.t<<" knight moves."<<endl;
			return;
		}
		//对下个节点进行标记 
		for(int i = 0;i < 8;i++){
			nextp.x = first.x + dir[i][0];
			nextp.y = first.y + dir[i][1];
			
			if(nextp.x < 0 || nextp.x >= 8 ||nextp.y < 0 || nextp.y >= 8 || map[nextp.x][nextp.y] == 1){
				continue;
			}
			map[nextp.x][nextp.y] = 1;
			nextp.t = first.t +1;
			//将节点加入队列当中 
			q.push(nextp);
			
		}
	}
}
 
int main(){
	ios::sync_with_stdio(false);
	while(cin>>a>>b){
		xa = a[0] - 'a';
		ya = a[1] - '1';
		xb = b[0] - 'a';
		yb = b[1] - '1';
		memset(map,0,sizeof(map));
		bfs(); 
	}
	
	return 0;
}



```
	
