---
layout:     post
title:      Equalize the Remainders
subtitle:  Equalize the Remainders-取余
date:       2018-06-30
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
---
[http://codeforces.com/contest/999/problem/D](http://codeforces.com/contest/999/problem/D)
# 问题描述：
You are given an array consisting of nn integers a1,a2,…,ana1,a2,…,an, and a positive integer mm. It is guaranteed that mm is a divisor of nn.

In a single move, you can choose any position ii between 11 and nn and increase aiai by 11.

Let's calculate crcr (0≤r≤m−1)0≤r≤m−1) — the number of elements having remainder rr when divided by mm. In other words, for each remainder, let's find the number of corresponding elements in aa with that remainder.

Your task is to change the array in such a way that c0=c1=⋯=cm−1=nmc0=c1=⋯=cm−1=nm.

Find the minimum number of moves to satisfy the above requirement.

**Input**
The first line of input contains two integers nn and mm (1≤n≤2⋅105,1≤m≤n1≤n≤2⋅105,1≤m≤n). It is guaranteed that mm is a divisor of nn.

The second line of input contains nn integers a1,a2,…,ana1,a2,…,an (0≤ai≤1090≤ai≤109), the elements of the array.

**Output**
In the first line, print a single integer — the minimum number of moves required to satisfy the following condition: for each remainder from 00to m−1m−1, the number of elements of the array having this remainder equals nmnm.

In the second line, print any array satisfying the condition and can be obtained from the given array with the minimum number of moves. The values of the elements of the resulting array must not exceed 10181018.

# 问题分析：
>题目大意是有n个数,m作为取模的数，可以对这n个数进行加一操作，要求使得这一列数对m取余后，相同余数的个数都等于m/n的值。

举个例子。
>6 3
3 2 0 6 10 12

其中n = 6,m = 3,t = m/n = 2;
初始列对3取余后的余数为：0,2，0,0,1,0
其中余数0的个数为4,1的个数为1，2的个数为1；因此对该数列进行适当的加操作，使得相同余数的个数都等于t值这里为2。
余数可以变为：1,2,2,0,1,0
因此结果为：
>3
4 2 2 6 10 12

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
 
const int N = 200005;
set<int>w;
set<int>::iterator it;
int get(int k){
	it = w.lower_bound(k);
	if(it == w.end()){
		return *w.begin();
	}
	return *it;
}
 
int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	int n,m,t;
	cin>>n>>m;
	t = n/m;
	int a[N];
	int q[N];
	long long step = 0;
	memset(q,0,sizeof(q));
	for(int i = 0;i < n;i++){
		cin>>a[i];
		//保存余数个数 
		q[a[i] % m]++;
	}
	for(int i = 0;i < m;i++){
		if(q[i] < t){
			//保存不足的余数 
			w.insert(i);
		}
	}
	for(int i = 0;i < n;i++){
		if(q[a[i] % m] > t){
			//找到下一个不足的余数 
			int k = get(a[i] % m);
			q[a[i] % m]--;
			q[k]++;
			//当余数个数满足时，set中删除余数 
			if(q[k] == t){
				w.erase(k);
			}
			//计算步长 
			int s = (k+m-a[i]%m)%m;
			a[i] += s;
			step += s;
		}
	}
	cout<<step<<endl;
	for(int i = 0;i < n-1;i++){
		cout<<a[i]<<" ";
	}
	cout<<a[n-1]<<endl;
	return 0;
}

```
