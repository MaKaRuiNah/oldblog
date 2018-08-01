---
layout:     post
title:      Mishka and Contest
subtitle:  Mishka and Contest-找k值
date:       2018-06-30
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
---
[http://codeforces.com/contest/999/problem/A](http://codeforces.com/contest/999/problem/A)
# 问题描述：
Mishka started participating in a programming contest. There are nn problems in the contest. Mishka's problem-solving skill is equal to kk.

Mishka arranges all problems from the contest into a list. Because of his weird principles, Mishka only solves problems from one of the ends of the list. Every time, he chooses which end (left or right) he will solve the next problem from. Thus, each problem Mishka solves is either the leftmost or the rightmost problem in the list.

Mishka cannot solve a problem with difficulty greater than kk. When Mishka solves the problem, it disappears from the list, so the length of the list decreases by 11. Mishka stops when he is unable to solve any problem from any end of the list.

How many problems can Mishka solve?

**Input**
The first line of input contains two integers nn and kk (1≤n,k≤1001≤n,k≤100) — the number of problems in the contest and Mishka's problem-solving skill.

The second line of input contains nn integers a1,a2,…,ana1,a2,…,an (1≤ai≤1001≤ai≤100), where aiai is the difficulty of the ii-th problem. The problems are given in order from the leftmost to the rightmost in the list.

**Output**
Print one integer — the maximum number of problems Mishka can solve.

# 问题分析：
>题目大意就是从n个值中从最左边找到第一个比k大的下标，或者可以从最右边找到第一个比k值大的数的下标。最后输出两个下标值分别到达边界的距离和。注意当输出与n值相等时，表示n个数都<=k.直接输出k值。

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
 
const int N = 1005;
 
int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	
	int n,k;
	cin>>n>>k;
	int a[105];
	for(int i = 0;i < n;i++){
		cin>>a[i];
	}
	int cnt = 0;
	//从左往右查找 
	for(int i = 0;i <n;i++){
		if(a[i] > k){
			break;
		}
		cnt++;
	}
	//从右往左查找 
	for(int i = n-1;i >= 0;i--){
		if(a[i] > k){
			break;
		}
		cnt++;
	}
	//所有值都比<=k 
	if(cnt > n)
	cnt /= 2;
	cout<<cnt<<endl;
	return 0;
}




```
	
