---
layout:     post
title:      Red and Black
subtitle: Red and Black-简单dfs
date:       2018-08-17
author:     Manson
header-img: img/gakki5.jpg
catalog: true
tags:
    - hdu
    - dfs
---
[http://acm.hdu.edu.cn/showproblem.php?pid=1312](http://acm.hdu.edu.cn/showproblem.php?pid=1312)

# 问题描述

There is a rectangular room, covered with square tiles. Each tile is colored either red or black. A man is standing on a black tile. From a tile, he can move to one of four adjacent tiles. But he can't move on red tiles, he can move only on black tiles.

Write a program to count the number of black tiles which he can reach by repeating the moves described above. 
 
**Input**

The input consists of multiple data sets. A data set starts with a line containing two positive integers W and H; W and H are the numbers of tiles in the x- and y- directions, respectively. W and H are not more than 20.

There are H more lines in the data set, each of which includes W characters. Each character represents the color of a tile as follows.

'.' - a black tile 
'#' - a red tile 
'@' - a man on a black tile(appears exactly once in a data set) 
 
**Output**

For each data set, your program should output a line which contains the number of tiles he can reach from the initial tile (including itself). 

# 问题分析
> 问题大意是 w*h的方格，有一个起点为黑色，他相邻的黑色能都走，不能走红色，问他能走多少格。
> 本题就是个简单的dfs，直接dfs遍历就行。

# AC代码


```

/*
author:Manson
date:8.17.2018
theme:dfs
*/
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 25;

int w,h;
char a[N][N];
int used[N][N];
int sx,sy,ans;
int dir[4][2] = {-1,0,0,-1,1,0,0,1};

void dfs(int x,int y){
	ans++;
	for(int i = 0;i < 4;i++){
		int xx = x + dir[i][0];
		int yy = y + dir[i][1];
		if(xx >= 0 && xx < h && yy >= 0 && yy < w &&
		!used[xx][yy] && a[xx][yy] != '#'){
			used[xx][yy] = 1;
			dfs(xx,yy);
		}
	}
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	while(cin>>w>>h){
		if(w == 0 && h == 0){
			break;
		}
		for(int i = 0;i < h;i++){
			for(int j = 0;j < w;j++){
				cin>>a[i][j];
			}
		}
		ans = 0;
		memset(used,0,sizeof(used));
		for(int i = 0;i < h;i++){
			for(int j = 0;j < w;j++){
				if(a[i][j] == '@'){
					sx = i;
					sy = j;
				}
			}
		}
		used[sx][sy] = 1;
		dfs(sx,sy);
		cout<<ans<<endl;
	}
	return 0;
}



```
