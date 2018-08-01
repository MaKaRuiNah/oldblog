---
layout:     post
title:      Snuke Numbers
subtitle: Snuke Numbers-求Snuke数
date:       2018-08-01
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - AtCoder
---
[https://arc099.contest.atcoder.jp/tasks/arc099_b](https://arc099.contest.atcoder.jp/tasks/arc099_b)

# 问题描述
Let S(n) denote the sum of the digits in the decimal notation of n. For example, S(123)=1+2+3=6.

We will call an integer n a Snuke number when, for all positive integers m such that m>n,  n	S(n) ≤ m	S(m)  holds.

Given an integer K, list the K smallest Snuke numbers.

**Constraints**

1≤K
The K-th smallest Snuke number is not greater than 1015.

**Input**

Input is given from Standard Input in the following format:
K

**Output**

Print K lines. The i-th line should contain the i-th smallest Snuke number.

# 问题分析
>问题大意是按照规则求前K个的Snuke数。这题的主要是找到数字规律是首位一次加一，其他位都为9时满足Snuke数。
这里列举出前20个Snuke数
1  2  3  4  5  6  7  8  9  19  29  39  49  59  69  79  89  99  199  299

# AC代码


```
/*
author:Manson
date:1.8.2018
theme:
*/
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1005;

ll fsum(ll x){
	ll a = 0;
	while(x){
		a += (x % 10);
		x /= 10;
	}
	return a;
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	vector<ll>v;
	for(int i = 1;i < 10;i++){
		v.push_back(i);
	}
	v.push_back(19);
	ll K;
	cin>>K;
	ll last = 19;
	while(v.size() < K){
		//去向量的最后一个fsum 
		ll p = fsum(last);
		ll add = 1;
		//99 :109 119 
		while((last+add)*fsum(last+add*2) > (last+2*add)*fsum(last+add)){
			add *= 10;
		}
		last += add;
		v.push_back(last);
	}
	for(int i = 0;i < K;i++){
		cout<<v[i]<<endl;
	}
	return 0;
}

```
