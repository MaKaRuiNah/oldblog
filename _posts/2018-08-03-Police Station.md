---
layout:     post
title:       Police Station
subtitle: Police Station-bfs，dfs问题
date:       2018-08-03
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
    - dfs
---
[http://codeforces.com/problemset/problem/208/C](http://codeforces.com/problemset/problem/208/C)

# 问题描述
The Berland road network consists of n cities and of m bidirectional roads. The cities are numbered from 1 to n, where the main capital city has number n, and the culture capital — number 1. The road network is set up so that it is possible to reach any city from any other one by the roads. Moving on each road in any direction takes the same time.
All residents of Berland are very lazy people, and so when they want to get from city v to city u, they always choose one of the shortest paths (no matter which one).
The Berland government wants to make this country's road network safer. For that, it is going to put a police station in one city. The police station has a rather strange property: when a citizen of Berland is driving along the road with a police station at one end of it, the citizen drives more carefully, so all such roads are considered safe. The roads, both ends of which differ from the city with the police station, are dangerous.
Now the government wonders where to put the police station so that the average number of safe roads for all the shortest paths from the cultural capital to the main capital would take the maximum value.

**Input**

The first input line contains two integers n and m (2 ≤ n ≤ 100, ) — the number of cities and the number of roads in Berland, correspondingly. Next m lines contain pairs of integers vi, ui (1 ≤ vi, ui ≤ n, vi ≠ ui) — the numbers of cities that are connected by the i-th road. The numbers on a line are separated by a space.
It is guaranteed that each pair of cities is connected with no more than one road and that it is possible to get from any city to any other one along Berland roads.

**Output**

Print the maximum possible value of the average number of safe roads among all shortest paths from the culture capital to the main one. The answer will be considered valid if its absolute or relative inaccuracy does not exceed 10 - 6.



# 问题分析
>问题大意是有n个点,m条边的有向图，现在要在一个点建一个警察局。一条边只要有一端与警察局相连，那么就认为该路是安全的路。**现在问在哪一个点建可以使得从1-n的每条最短路上平均的安全道路（每条最短路的安全路条数之和/最短路的条数）最多**
>这个问题的解决思路主要是用bfs，两次bfs，分别从1和 n 开始。用 c[0][i] 表示从1到i的最短路径条数  ，d[0][i]表示从1到i的最短 路径长度 ； c[1][i] 表示从n到i的最短路径条数  ，d[1][i]表示从n到i的最短 路径长度 。最后在 i 点处的平均安全道路的条数为**2.0*( c[0][i]*c[1][i] ) /  c[0][n]**；求出最大的那个值。

 
# AC代码


```
/*
author:Manson
date:8.3.2018
theme:
*/
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const int N = 105;

int used[N];
vector<int>a[N];
ll c[2][N];//c[0][i]表示从1到i的最短路径条数 
ll d[2][N];//d[0][i]表示从1到i的最短 路径长度 
int m,n;

void bfs(int id,int s){
	queue<int>q;
	d[id][s] = 0;
	c[id][s] = 1;
	memset(used,0,sizeof(used));
	q.push(s);
	used[s] = 1;
	int u,v;
	while(!q.empty()){
		u = q.front();
		q.pop();
		for(int i = 0;i < a[u].size();i++){
			v = a[u][i];
			if(!used[v]){
				used[v] = 1;
				//未访问过的节点 
				d[id][v] = d[id][u]+1;
				c[id][v] = c[id][u];
				q.push(v);
			}
			//关键路径上的节点 
			else if(d[id][v] == d[id][u] + 1){
				c[id][v] += c[id][u];
			}
		}
	}
} 

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	cin>>n>>m;
	int u,v;
	for(int i = 0;i <m;i++){
		cin>>u>>v;
		a[u].push_back(v);
		a[v].push_back(u);
	}
	//从1到i bfs 
	bfs(0,1);
	//从n到i bfs 
	bfs(1,n);
	double ans = 1.0;
	for(int i = 2;i < n;i++){
		if(d[0][i] + d[1][i] == d[0][n]){
			ans = max(ans,2.0*(c[0][i]*c[1][i])/ c[0][n]);
			//cout<<ans<<endl;
		}
	}
	cout<<setprecision(12)<<fixed<<ans<<endl;
	return 0;
}


```
