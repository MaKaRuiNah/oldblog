---
layout:     post
title:      Bitter Alchemy
subtitle:  简单甜甜圈问题
date:       2018-05-05
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - AtCoder
---
[https://abc095.contest.atcoder.jp/tasks/abc095_b](https://abc095.contest.atcoder.jp/tasks/abc095_b)
# 问题描述：
Akaki, a patissier, can make N kinds of doughnut using only a certain powder called "Okashi no Moto" (literally "material of pastry", simply called Moto below) as ingredient. These doughnuts are called Doughnut 1, Doughnut 2, …, Doughnut N. In order to make one Doughnut i (1≤i≤N), she needs to consume mi grams of Moto. She cannot make a non-integer number of doughnuts, such as 0.5 doughnuts.

Now, she has X grams of Moto. She decides to make as many doughnuts as possible for a party tonight. However, since the tastes of the guests differ, she will obey the following condition:

For each of the N kinds of doughnuts, make at least one doughnut of that kind.
At most how many doughnuts can be made here? She does not necessarily need to consume all of her Moto. Also, under the constraints of this problem, it is always possible to obey the condition.

# 问题分析：
>问题大意就是共有N种甜甜圈，总量为X克，每种至少有一个，且要尽可能的多的数量的甜甜圈。


# AC代码：

```c++

#include<iostream>
#include<cmath>
using namespace std;
#include<iomanip>
#include<algorithm>
const int N = 102;
int main(){
	ios::sync_with_stdio(false);
	int n,k;
	int a[N];
	cin>>n>>k;
	for(int i = 0;i < n;i++){
		cin>>a[i];
		k -= a[i];
	}
	sort(a,a+n);
	cout<<n+k/a[0]<<endl;
	return 0;
}



```
	
