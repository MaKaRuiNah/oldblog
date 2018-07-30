---
layout:     post
title:      Integer Inquiry
subtitle:  Integer Inquiry（高精度问题）
date:       2018-03-18
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - hdu
    - 高精度
---
# 问题描述：
[http://acm.hdu.edu.cn/showproblem.php?pid=1047](http://acm.hdu.edu.cn/showproblem.php?pid=1047)
One of the first users of BIT's new supercomputer was Chip Diller. He extended his exploration of powers of 3 to go from 0 to 333 and he explored taking various sums of those numbers. 
`This supercomputer is great,' remarked Chip. ``I only wish Timothy were here to see these results.'' (Chip moved to a new apartment, once one became available on the third floor of the Lemon Sky apartments on Third Street.) 
The input will consist of at most 100 lines of text, each of which contains a single VeryLongInteger. Each VeryLongInteger will be 100 or fewer characters in length, and will only contain digits (no VeryLongInteger will be negative). 

The final input line will contain a single zero on a line by itself.

sample: 
1

    123456789012345678901234567890

    123456789012345678901234567890

    1234567890123456789012345678900

    0

# 问题分析：
>本题主要是对大数模板的套用，直接简单地套用大数模板就可AC这道题了。

# AC代码：

```c++

#include<iostream>
using namespace std;
#include <cstring>
#define MAXN 9999
#define DLEN 4
 
int a[105];
int b[105];
char s1[105];
int len,len1;
void add_str(char *s){
	memset(b,0,sizeof(b));
	int l;
	int index = 0;
	l = strlen(s);
	len1 = l/4;
	if(l%4){
		len1++;
	}
	len = (len >len1)?len:len1;
	//将字符转化为数 
	for(int i = l-1;i >= 0;i-=4){
		int k = i-3;
		if(k < 0)
		k = 0;
		int t = 0;
		for(int j = k;j <= i;j++){
			t = (s[j]-'0')+t*10; 
		}
		b[index++] = t;
	}
	//大整数相加 
	for(int i = 0;i < len;i++){
		a[i] += b[i];
		if(a[i] > MAXN){
			a[i] -= (MAXN+1);
			a[i+1]++;
		}
	}
	if(a[len] == 0){
		len--;
	}
}
 
int main()
{
	ios::sync_with_stdio(false);
	
	int t;
	cin>>t;
	while(t--){
		memset(a,0,sizeof(a));
		len = 0;
		while(cin>>s1){
			if(s1[0] == '0')
			break;
			add_str(s1);
		}
		cout<<a[len]; 
		for(int i = len-1;i >= 0;i--){
			cout.width(4);
			cout.fill('0');
			cout<<a[i];
		}
		cout<<endl;
		if(t > 0)
		cout<<endl;
	}
	return 0;
}





```
	
