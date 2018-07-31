---
layout:     post
title:      Alphabetic Removals
subtitle:  Alphabetic Removals-字符删除
date:       2018-06-30
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
---
[http://codeforces.com/contest/999/problem/C](http://codeforces.com/contest/999/problem/C)
# 问题描述：
You are given a string ss consisting of nn lowercase Latin letters. Polycarp wants to remove exactly kk characters (k≤nk≤n) from the string ss. Polycarp uses the following algorithm kk times:

if there is at least one letter 'a', remove the leftmost occurrence and stop the algorithm, otherwise go to next item;
if there is at least one letter 'b', remove the leftmost occurrence and stop the algorithm, otherwise go to next item;
...
remove the leftmost occurrence of the letter 'z' and stop the algorithm.
This algorithm removes a single letter from the string. Polycarp performs this algorithm exactly kk times, thus removing exactly kk characters.

Help Polycarp find the resulting string.

**Input**
The first line of input contains two integers nn and kk (1≤k≤n≤4⋅1051≤k≤n≤4⋅105) — the length of the string and the number of letters Polycarp will remove.

The second line contains the string ss consisting of nn lowercase Latin letters.

**Output**
Print the string that will be obtained from ss after Polycarp removes exactly kk letters using the above algorithm kk times.

If the resulting string is empty, print nothing. It is allowed to print nothing or an empty line (line break).

# 问题分析：
>从a到z顺序删除，一直到删除了k个字符为止。输出删除后的字符。

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
 
const int N = 400005;
 
int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	int n,k;
	string s;
	cin>>n>>k>>s;
	int flag[N];
	memset(flag,1,sizeof(flag));
	for(int i = 0;i < 26;i++){
		for(int j = 0;j < s.size();j++){
			//从a开始删除 
			if(s[j] == 'a'+i && k > 0){
				k--;
				//标记已经删除了的字符 
				flag[j] = 0;
			}
		}
	}
	for(int i = 0;i < s.size();i++){
		if(flag[i]){
			cout<<s[i];
		}
	}
	cout<<endl;
	return 0;
}

```
