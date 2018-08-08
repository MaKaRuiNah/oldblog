---
layout:     post
title:      Distance in Tree
subtitle: Distance in Tree-dfs问题
date:       2018-08-08
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
    - dfs
---
[https://codeforces.com/contest/161/problem/D#](https://codeforces.com/contest/161/problem/D#)

# 问题描述

A tree is a connected graph that doesn't contain any cycles.

The distance between two vertices of a tree is the length (in edges) of the shortest path between these vertices.

You are given a tree with n vertices and a positive number k. Find the number of distinct pairs of the vertices which have a distance of exactly k between them. Note that pairs (v, u) and (u, v) are considered to be the same pair.

**Input**

The first line contains two integers n and k (1 ≤ n ≤ 50000, 1 ≤ k ≤ 500) — the number of vertices and the required distance between the vertices.

Next n - 1 lines describe the edges as "ai bi" (without the quotes) (1 ≤ ai, bi ≤ n, ai ≠ bi), where ai and bi are the vertices connected by the i-th edge. All given edges are different.

**Output**
Print a single integer — the number of distinct pairs of the tree's vertices which have a distance of exactly k between them.

Please do not use the %lld specifier to read or write 64-bit integers in С++. It is preferred to use the cin, cout streams or the %I64d specifier.

**e.g.**
5 2
1 2
2 3
3 4
2 5

12

# 问题分析
>问题大意是 有一棵树，求距离为k的点对有多少个。
>本题的解题思路主要还是dfs。用dis[i][j]表示距离点i路长为j的点的个数。long long ans更新距离为k的点的个数。ans += dis[v][j] * dis[u][k-j-1];表示距离v点长为j的点个数 * 距离u点长为 k-j-1的点个数 。

 
# AC代码


```
/*

/*
author:Manson
date:8.8.2018
theme:
*/
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 50010;

vector<ll>g[N];
int used[N];
//dis[i][j]表示 距离点 i 路长为 j 的点 个数 
ll dis[N][505];
ll ans;
int n,k;
void dfs(int v){
	
	int u;
	memset(dis[v],0,sizeof(dis[v]));
	dis[v][0] = 1;
	for(int i = 0;i < g[v].size();i++){
		u = g[v][i];
		if(used[u] == 0){
			used[u] = 1;
			dfs(u);
			for(int j = 0;j < k;j++){
				//距离v点长为j的个数 * 距离u点长为 k-j-1的个数 
				ans += (dis[v][j]*dis[u][k-j-1]);
			}
			//到v点距离为j的点的个数 = 到u点距离为j-1的点的个数 
			for(int j = 1;j <= k;j++){
				dis[v][j] += dis[u][j-1];
			}
		}
	}
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	
	int a,b;
	cin>>n>>k;
	for(int i = 0;i < n-1;i++){
		cin>>a>>b;
		g[a].push_back(b);
		g[b].push_back(a);
	}
	ans = 0;
	memset(used,0,sizeof(used));
	used[1] = 1;
	dfs(1);
	cout<<ans<<endl;
	return 0;
}


```
