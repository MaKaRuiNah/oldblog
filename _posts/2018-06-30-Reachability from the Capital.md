---
layout:     post
title:      Reachability from the Capital
subtitle:  Reachability from the Capital-到达中心点的路径
date:       2018-06-30
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
---
[http://codeforces.com/contest/999/problem/E](http://codeforces.com/contest/999/problem/E)
# 问题描述：
There are nn cities and mm roads in Berland. Each road connects a pair of cities. The roads in Berland are one-way.

What is the minimum number of new roads that need to be built to make all the cities reachable from the capital?

New roads will also be one-way.

**Input**
The first line of input consists of three integers nn, mm and ss (1≤n≤5000,0≤m≤5000,1≤s≤n1≤n≤5000,0≤m≤5000,1≤s≤n) — the number of cities, the number of roads and the index of the capital. Cities are indexed from 11 to nn.

The following mm lines contain roads: road ii is given as a pair of cities uiui, vivi (1≤ui,vi≤n1≤ui,vi≤n, ui≠viui≠vi). For each pair of cities (u,v)(u,v), there can be at most one road from uu to vv. Roads in opposite directions between a pair of cities are allowed (i.e. from uu to vv and from vv to uu).

**Output**
Print one integer — the minimum number of extra roads needed to make all the cities reachable from city ss. If all the cities are already reachable from ss, print 0.

# 问题分析：
>本道题的大意是给你一张有向图，需要使得给定的点可以到达图中任意的一个节点位置，问至少有在图中修多少条路。

The first example is illustrated by the following:
![http://codeforces.com/predownloaded/b4/d4/b4d4da8cba4ea7c31a2c2d085db74a1052ed6603.png](http://codeforces.com/predownloaded/b4/d4/b4d4da8cba4ea7c31a2c2d085db74a1052ed6603.png)

***For example, you can add roads (6,46,4), (7,97,9), (1,71,7) to make all the cities reachable from s=1s=1.***

本道题的解题思想主要是dfs。首先我们遍历1到n个点，把到达过的位置做一个标记，并将每个点可以到达的位置保存到堆栈中。然后标记清零，bfs定点s可以到达的节点，做标记。堆栈中未被标记的位置便是需要建立通路的位置。

# AC代码：

```c++

#include <iostream>
#include<iomanip>
#include<cstring>
#include<cstdio>
#include<cmath>
#include<algorithm>
#include<set>
#include<stack>
#include<queue>
using namespace std;
 
const int N = 5005;
 
int m,n,s;
int a[N];
int used[N];
vector<int>G[N];
stack<int>st;
//遍历每个点所能达到的节点位置，并保存 
void dfs(int u){
	used[u] = 1;
	/*
	for(int v:G[u])
        if(!vis[v])
            dfs(v);
    st.push(u);
    */
	for(int i = 0;i < G[u].size();i++){
		int v = G[u][i];
		if(!used[v]){
			dfs(v);
		}
	}
	st.push(u);
}
 
void dfs1(int v){
	used[v] = 1;
	for(int i = 0;i < G[v].size();i++){
		int u = G[v][i];
		if(!used[u]){
			dfs(u);
		}
	}
}
 
int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	cin>>n>>m>>s;
	int a,b;
	memset(used,0,sizeof(used));
	for(int i = 1;i <= m;i++){
		cin>>a>>b;
		//从a到b有路 
		G[a].push_back(b);
	}
	for(int i= 1;i <= n;i++){
		if(!used[i]){
			//遍历每个点 
			dfs(i);
		}
	}
	memset(used,0,sizeof(used));
	dfs1(s);
	int cnt = 0;
	while(!st.empty()){
		int u = st.top();
		st.pop();
		if(!used[u]){
			dfs1(u);
			cnt++;
		} 
	}
	cout<<cnt<<endl;
	return 0;
}


```
