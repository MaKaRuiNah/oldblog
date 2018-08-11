---
layout:     post
title:      Mysterious Present
subtitle: Mysterious Present-动态规划
date:       2018-08-10
author:     Manson
header-img: img/gakki3.jpg
catalog: true
tags:
    - codeforces
    - 动态规划
---
[http://codeforces.com/contest/4/problem/D](http://codeforces.com/contest/4/problem/D)

# 问题描述

Peter decided to wish happy birthday to his friend from Australia and send him a card. To make his present more mysterious, he decided to make a chain. Chain here is such a sequence of envelopes A = {a1,  a2,  ...,  an}, where the width and the height of the i-th envelope is strictly higher than the width and the height of the (i  -  1)-th envelope respectively. Chain size is the number of envelopes in the chain.

Peter wants to make the chain of the maximum size from the envelopes he has, the chain should be such, that he'll be able to put a card into it. The card fits into the chain if its width and height is lower than the width and the height of the smallest envelope in the chain respectively. It's forbidden to turn the card and the envelopes.

Peter has very many envelopes and very little time, this hard task is entrusted to you.

**Input**
The first line contains integers n, w, h (1  ≤ n ≤ 5000, 1 ≤ w,  h  ≤ 106) — amount of envelopes Peter has, the card width and height respectively. Then there follow n lines, each of them contains two integer numbers wi and hi — width and height of the i-th envelope (1 ≤ wi,  hi ≤ 106).

**Output**
In the first line print the maximum chain size. In the second line print the numbers of the envelopes (separated by space), forming the required chain, starting with the number of the smallest envelope. Remember, please, that the card should fit into the smallest envelope. If the chain of maximum size is not unique, print any of the answers.

If the card does not fit into any of the envelopes, print number 0 in the single line.

# 问题分析
>问题大意是 有一个信封序列，要求满足卡片的长宽都小于信封的长宽，且第i个信封序列的长宽都大于第i-1个信封的长宽。要求满足条件的最长信封序列。

>这个问题明显属于动态规划问题。这里我用 f[i] 来表示前i个信封能满足条件的最大信封个数。g[i]表示满足信封序列第i个信封的 前一个信封序列号。输出时用递归输出。**f[i] = max(f[j]+1); (0<=j<i)**
 
# AC代码


```

/*
author:Manson
date:8.10.2018
theme:动态规划 
*/
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 5005;
//f[i]表示第i个信封前能放入卡片的信封个数 
//g[i]表示满足信封序列第i个信封的 前一个信封序列号

int f[N],g[N];
int n,x,y,ans;

struct node{
	int id;
	int x;
	int y;
	bool operator<(const node &aa) const{
		if(y == aa.y){
			return y < aa.y;
		}
		return x < aa.x;
	}
}a[N];

void Index(int ix){
	if(ix == -1)
	return;
	Index(g[ix]);
	cout<<a[ix].id<<" ";
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	cin>>n>>x>>y;
	for(int i = 0;i < n;i++){
		cin>>a[i].x>>a[i].y;
		a[i].id = i+1;
	}
	sort(a,a+n);
	memset(f,0,sizeof(f));
	memset(g,-1,sizeof(g));

	for(int i = 0;i < n;i++){
		if(a[i].x > x && a[i].y > y){
			f[i] = 1;
			for(int j = 0;j < i;j++){
				if(a[j].x < a[i].x &&a[j].y < a[i].y && f[j] >= f[i]){
					f[i] = f[j]+1;
					g[i] = j;
				}
			}
			if(f[ans] < f[i]){
				ans = i;
			}
		}
	}
	cout<<f[ans]<<endl;
	if(f[ans]){
		Index(ans);
	}

	return 0;
}



```
