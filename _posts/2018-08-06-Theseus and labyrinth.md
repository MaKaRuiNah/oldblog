---
layout:     post
title:      Theseus and labyrinth
subtitle: Theseus and labyrinth-bfs问题
date:       2018-08-06
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
    - bfs
---
[https://codeforces.com/contest/676/problem/D](https://codeforces.com/contest/676/problem/D)





# 问题分析
>问题大意是 主人公从一个起点走到一个终点。每一个点的四周有门或墙，只有两个们相对是才能走通。当然也可以停下一秒，使得所有的门都旋转90°。问从起点到达终点所需要的最短路径。
>这里我们可以用g[x][y],表示点(x,y)的可走方向。used[x][y][5]表示方向是否走过。然后用bfs可以模拟过程，求出所需的最短时间。

 
# AC代码


```
/*
author:Manson
date:8.6.2018
theme:Theseus and labyrinth
*/
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1005;

char c;  
int g[N][N];  // g[x][y]:用二进制存放(x, y)点处的可走方向，亮点 
int	n,m;

int dir[4][2] ={{0,-1},{1,0},{0,1},{-1,0}};  
int used[N][N][5];  // 标志是否走过 

struct node{  
    int u,v;   	// 位置 
	int time;	// 所走的步数 
	int	state; 	// 旋转次数%4 
    node():time(0){};  
    node(int _u, int _v, int _time, int _state):u(_u),v(_v),time(_time),state(_state){}  
}s,t;

int fun(char x){  
    switch(x){  
    case '^': return 8; break;  
    case 'v': return 2; break;  
    case '<': return 1; break;  
    case '>': return 4; break;  
    case '+': return 15;break;  
    case '-': return 5; break;  
    case '|': return 10;break;  
    case 'L': return 14;break;  
    case 'R': return 11;break;  
    case 'U': return 7; break;  
    case 'D': return 13;break;  
    case '*': return 0; break;  
    }  
} 

int dfs(){
	memset(used,0,sizeof(used));
	queue<node>q;
	node next;
	node head;
	q.push(s);
	used[s.u][s.v][s.state] = 1;
	while(!q.empty()){
		head = q.front();
		q.pop();
		//到达终点 
		if(head.u == t.u && head.v == t.v){
			return head.time;
		}
		//顺时针方向旋转一次 
		if(!used[head.u][head.v][(head.state+1)%4]){
			q.push(node(head.u,head.v,head.time+1,(head.state+1)%4));
			used[head.u][head.v][(head.state+1)%4] = 1;
		}
		//四个方向一一判定 
		for(int i = 0;i < 4;i++){
			next.u= head.u+dir[i][0];
			next.v = head.v+dir[i][1];
			if(g[next.u][next.v]!=0){
				next.state = head.state;
				//越界；在i方向有门；在i+2方向有门 
				if(next.u >= 1 && next.u <= n && next.v >= 1 && next.v<= m &&   
				   g[head.u][head.v] & ((1<<(i+next.state)%4)) &&
                   g[next.u][next.v] & ((1<<(i+next.state+2)%4))){
					if(!used[next.u][next.v][next.state]){
						next.time = head.time+1;
						q.push(next);
						used[next.u][next.v][next.state] = 1;
					}
				}
				
			}
		}
	}
	return -1;
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	
	while(cin>>n>>m){
		for(int i = 1;i <= n;i++){
			for(int j = 1;j <= m;j++){
				cin>>c;
				g[i][j] = fun(c); 
			} 
		}
		cin>>s.u>>s.v;
		cin>>t.u>>t.v;
		s.state = t.state = 0;
		cout<<dfs()<<endl;
	}
	
	return 0;
}



```
