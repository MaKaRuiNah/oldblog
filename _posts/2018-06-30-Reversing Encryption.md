---
layout:     post
title:      Reversing Encryption
subtitle:  Reversing Encryption-字符串翻转
date:       2018-06-30
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
---
[http://codeforces.com/contest/999/problem/B](http://codeforces.com/contest/999/problem/B)
# 问题描述：
A string ss of length nn can be encrypted by the following algorithm:

iterate over all divisors of nn in decreasing order (i.e. from nn to 11),
for each divisor dd, reverse the substring s[1…d]s[1…d] (i.e. the substring which starts at position 11 and ends at position dd).
For example, the above algorithm applied to the string ss="codeforces" leads to the following changes: "codeforces" →→"secrofedoc" →→ "orcesfedoc" →→ "rocesfedoc" →→ "rocesfedoc" (obviously, the last reverse operation doesn't change the string because d=1d=1).

You are given the encrypted string tt. Your task is to decrypt this string, i.e., to find a string ss such that the above algorithm results in string tt. It can be proven that this string ss always exists and is unique.

**Input**
The first line of input consists of a single integer nn (1≤n≤1001≤n≤100) — the length of the string tt. The second line of input consists of the string tt. The length of tt is nn, and it consists only of lowercase Latin letters.

**Output**
Print a string ss such that the above algorithm results in tt.

# 问题分析：
>题目大意就是从1到n遍历，遇到n的因子就把字符串翻转。

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
	int n;
	string s;
	cin>>n>>s;
	
	for(int i = 1;i <= n;i++){
		if(n % i == 0){
			reverse(s.begin(),s.begin()+i);
		}
	}
	cout<<s<<endl;
	return 0;
}


```
**python:**

```
n, t = int(input()), input()
for i in range(1, n+1):
    if n % i == 0: t = t[i-1::-1] + t[i:]
print(t)

```
