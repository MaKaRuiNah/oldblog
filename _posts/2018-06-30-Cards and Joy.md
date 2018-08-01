---
layout:     post
title:      Cards and Joy
subtitle: Cards and Joy-卡片里获得的愉悦感
date:       2018-06-30
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
    - 动态规划
---
[http://codeforces.com/contest/999/problem/F](http://codeforces.com/contest/999/problem/F)
# 问题描述：
There are nn players sitting at the card table. Each player has a favorite number. The favorite number of the jj-th player is fjfj.

There are k⋅nk⋅n cards on the table. Each card contains a single integer: the ii-th card contains number cici. Also, you are given a sequence h1,h2,…,hkh1,h2,…,hk. Its meaning will be explained below.

The players have to distribute all the cards in such a way that each of them will hold exactly kk cards. After all the cards are distributed, each player counts the number of cards he has that contains his favorite number. The joy level of a player equals htht if the player holds tt cards containing his favorite number. If a player gets no cards with his favorite number (i.e., t=0t=0), his joy level is 00.

Print the maximum possible total joy levels of the players after the cards are distributed. Note that the sequence h1,…,hkh1,…,hk is the same for all the players.

**Input**

The first line of input contains two integers nn and kk (1≤n≤500,1≤k≤101≤n≤500,1≤k≤10) — the number of players and the number of cards each player will get.

The second line contains k⋅nk⋅n integers c1,c2,…,ck⋅nc1,c2,…,ck⋅n (1≤ci≤1051≤ci≤105) — the numbers written on the cards.

The third line contains nn integers f1,f2,…,fnf1,f2,…,fn (1≤fj≤1051≤fj≤105) — the favorite numbers of the players.

The fourth line contains kk integers h1,h2,…,hkh1,h2,…,hk (1≤ht≤1051≤ht≤105), where htht is the joy level of a player if he gets exactly tt cards with his favorite number written on them. It is guaranteed that the condition ht−1<htht−1<ht holds for each t∈[2..k]t∈[2..k].

**Output**

Print one integer — the maximum possible total joy levels of the players among all possible card distributions.

# 问题分析：
>这题明显是一道动态规划问题，用dp[i][j]表示某一个数可以让人获得的最大满足感，其中 i表示某一个数在n*k个数中一共有i个数，j表示这个数是人喜欢的数在n个数中有j个。状态转移方程为:dp[i][j] = max(dp[i][j],dp[i-w][j-1]+h[i])


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
 
const int N = 100005;
 
int n,k;
int c[N],f[N],h[15];
long long dp[5050][5050];
long long getdp(int a,int b){
	if(a <= 0 || b <= 0)
	return 0;
	long long &res = dp[a][b];
	if(res != -1)
	return res;
	res = 0;
	for(int i = 0;i <= min(a,k);i++){
		//状态转移方程 
		res = max(res,h[i]+getdp(a-i,b-1));
	}
	return res;
}
 
int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	cin>>n>>k;
	for(int i = 0;i < k*n;i++){
		int x;
		cin>>x;
		c[x]++;
	}
	for(int i = 0;i < n;i++){
		int x;
		cin>>x;
		f[x]++;
	}
	for(int i = 1;i <= k;i++){
		cin>>h[i];
	}
	long long ans = 0;
	memset(dp,-1,sizeof(dp));
	for(int i = 1;i <= 100000;i++){
		ans += getdp(c[i],f[i]);	
	}
	cout<<ans<<endl;
	return 0;
}


```
