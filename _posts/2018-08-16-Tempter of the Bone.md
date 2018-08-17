---
layout:     post
title:      Tempter of the Bone
subtitle: Tempter of the Bone-dfs+奇偶剪枝
date:       2018-08-16
author:     Manson
header-img: img/gakki3.jpg
catalog: true
tags:
    - hdu
    - dfs
---
[http://acm.hdu.edu.cn/showproblem.php?pid=1010](http://acm.hdu.edu.cn/showproblem.php?pid=1010)

# 问题描述

The doggie found a bone in an ancient maze, which fascinated him a lot. However, when he picked it up, the maze began to shake, and the doggie could feel the ground sinking. He realized that the bone was a trap, and he tried desperately to get out of this maze.

The maze was a rectangle with sizes N by M. There was a door in the maze. At the beginning, the door was closed and it would open at the T-th second for a short period of time (less than 1 second). Therefore the doggie had to arrive at the door on exactly the T-th second. In every second, he could move one block to one of the upper, lower, left and right neighboring blocks. Once he entered a block, the ground of this block would start to sink and disappear in the next second. He could not stay at one block for more than one second, nor could he move into a visited block. Can the poor doggie survive? Please help him.
 
**Input**

The input consists of multiple test cases. The first line of each test case contains three integers N, M, and T (1 < N, M < 7; 0 < T < 50), which denote the sizes of the maze and the time at which the door will open, respectively. The next N lines give the maze layout, with each line containing M characters. A character is one of the following:

'X': a block of wall, which the doggie cannot enter; 
'S': the start point of the doggie; 
'D': the Door; or
'.': an empty block.

The input is terminated with three 0's. This test case is not to be processed.
 
**Output**

For each test case, print in one line "YES" if the doggie can survive, or "NO" otherwise.
# 问题分析
> 问题大意是 n*n的迷宫，有一个起点和终点，问给定t的时间是否能够正好从起点走到终点。
> 本题主要是dfs解法，bfs无法使用，因为不是求最短路径。剪枝市主要是奇偶剪枝，所求的路径与最短路径之差应为偶数。假设最短路径是先向下，再向右的一条路径话，而我们所求路径如果向上或者向左的话必须要再次向下，向右，因此差值是偶数，因此要用奇偶剪枝。

# AC代码


```

/*
author:Manson
date:8.16.2018
theme:dfs,奇偶剪枝 
*/
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 10;

char a[N][N];
int n,m,t;
int dir[4][2] = {-1,0,0,-1,1,0,0,1};
int flag;
int sx,sy,ex,ey;
//x表示墙的数量 
int x;
int used[N][N];

void dfs(int x,int y,int t1){
	if(ex == x && ey == y && t == t1){
		flag = 1;
		return;
	}
	if(flag){
		return;
	}
	//与最短路径时间差 
	int t2 = (t-t1) - (abs(x-ex)+abs(y-ey));
	if(t2 < 0 || t2&1){
		return;
	}
	for(int i = 0;i < 4;i++){
		int xx = x+dir[i][0];
		int yy = y+dir[i][1];
		if(xx >=0 && xx < n && yy >= 0 && yy < m && 
		!used[xx][yy] && a[xx][yy]!='X'){
			used[xx][yy] = 1;
			dfs(xx,yy,t1+1);
			used[xx][yy] = 0;
		}
	}
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	while(cin>>n>>m>>t){
		if(n == 0 && m == 0){
			break;
		}
		x = 0;
		for(int i = 0;i < n;i++){
			for(int j = 0;j < m;j++){
				cin>>a[i][j];
				if(a[i][j] == 'X'){
					x++;
				}
				else if(a[i][j] == 'S'){
					sx = i;
					sy = j;
				}
				else if(a[i][j] == 'D'){
					ex = i;
					ey = j;
				}
			}
		}
		if(n * m - t <= x){
			cout<<"NO"<<endl;
			continue;
		}
		flag = 0;
		memset(used,0,sizeof(used));
		used[sx][sy] = 1;
		dfs(sx,sy,0);
		if(flag){
			cout<<"YES"<<endl;
		}
		else{
			cout<<"NO"<<endl; 
		}
		
	}
	return 0;
}



```
