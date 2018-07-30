---
layout:     post
title:      A + B Problem II
subtitle:   A + B Problem II（高精度问题）
date:       2018-03-11
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - hdu
    - 高精度
---
# 问题描述：
I have a very simple problem for you. Given two integers A and B, your job is to calculate the Sum of A + B.
 
The first line of the input contains an integer T(1<=T<=20) which means the number of test cases. Then T lines follow, each line consists of two positive integers, A and B. Notice that the integers are very large, that means you should not process them by using 32-bit integer. You may assume the length of each integer will not exceed 1000.
# 问题分析：
>这道问题明显是两个大整数相加，我们可以直接利用高精度模板。鉴于这道题只考虑大数相加，于是我们可以简单利用两个数组分别表示大数。数组对应的下标表示不同的位数。

# AC代码：

```c++

#include<iostream>
using namespace std;
#include <cmath>
#include <cstring>
#define N 1001
int main(){
	int t;
	cin>>t;
	char c1[N],c2[N];
	int a[N],b[N],c[N];
	int len1,len2,len;
	for(int i = 1;i <= t;i++){
		memset(a,0,sizeof(a));
		memset(b,0,sizeof(b));
		memset(c,0,sizeof(c));
		cin>>c1>>c2;
		len1 = strlen(c1);
		len2 = strlen(c2);
		len = max(len1,len2);
		for(int j = len1 - 1;j >= 0;j--){
			a[len1-1-j] = c1[j] - '0';
		}
		for(int j = len2-1;j >= 0;j--){
			b[len2-1-j] = c2[j] - '0';
		}
		for(int j = 0; j < len;j++){
			c[j] = a[j]+b[j]+c[j];
			if(c[j] >= 10){
				c[j] -= 10;
				c[j+1]++;
			}
		}
		if(c[len] == 0){
			len--;
		}
		cout<<"Case "<<i<<":\n"<<c1<<" + "<<c2<<" = ";
		for(int j = len;j >= 0;j--){
			cout<<c[j];
		}
		if(i != t)
		cout<<endl<<endl;
		else
		cout<<endl;
	}
	return 0;
}



```
	
