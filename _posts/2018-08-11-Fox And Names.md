---
layout:     post
title:      Fox And Names
subtitle: Fox And Names-bfs
date:       2018-08-11
author:     Manson
header-img: img/gakki3.jpg
catalog: true
tags:
    - codeforces
    - bfs
---
[http://codeforces.com/contest/510/problem/C](http://codeforces.com/contest/510/problem/C)

# 问题描述

Fox Ciel is going to publish a paper on FOCS (Foxes Operated Computer Systems, pronounce: "Fox"). She heard a rumor: the authors list on the paper is always sorted in the lexicographical order.

After checking some examples, she found out that sometimes it wasn't true. On some papers authors' names weren't sorted in lexicographical order in normal sense. But it was always true that after some modification of the order of letters in alphabet, the order of authors becomes lexicographical!

She wants to know, if there exists an order of letters in Latin alphabet such that the names on the paper she is submitting are following in the lexicographical order. If so, you should find out any such order.

Lexicographical order is defined in following way. When we compare s and t, first we find the leftmost position with differing characters: si ≠ ti. If there is no such position (i. e. s is a prefix of t or vice versa) the shortest string is less. Otherwise, we compare characters si and ti according to their order in alphabet.

**Input**

The first line contains an integer n (1 ≤ n ≤ 100): number of names.

Each of the following n lines contain one string namei (1 ≤ |namei| ≤ 100), the i-th name. Each name contains only lowercase Latin letters. All names are different.

**Output**

If there exists such order of letters that the given names are sorted lexicographically, output any such order as a permutation of characters 'a'–'z' (i. e. first output the first letter of the modified alphabet, then the second, and so on).

Otherwise output a single word "Impossible" (without quotes).


# 问题分析
>问题大意是 有n个字符串，问是否存在一个字典序列满足这些字符串按照最小字典序排序。
>这题我认为可以使用bfs解。首先直接比较第i个字符串与第i+1个字符串。这样直接扫描就ok。扫描过程中，要用g[i]保存其字典序满足的条件，表示应排在 i 字符后面的字符；然后用index存储应排在i字符后面的字符个数。
>最后直接用bfs,优先取出正常字符序列，然后依次取出满足所给字符串字典序的字符。
 
# AC代码


```

/*
author:Manson
date:8.11.2018
theme:
*/
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 105;

int n;
string s[N];
int used[27];
//index数组保存着 所给字符串对应的排列方式。
//如 sad,happy,min那么index['s'-'h'] = 1 
int index[N];
//g[i]表示在字符 i 之后的字符 
vector<int>g[N];
int cnt = 0;

void bfs(){
	queue<int>q;
	//放入正常顺序的字符. 
	for(int i = 0;i < 26;i++){
		if(index[i] == 0){
			q.push(i);
		}
	}
	vector<char>ans;
	while(!q.empty()){
		cnt++;
		int top = q.front();
		q.pop();
		ans.push_back('a'+top);
		for(int x:g[top]){
			index[x]--;
			if(index[x] == 0){
				q.push(x);
			}
		}
	}
	if(cnt!=26){
		cout<<"Impossible"<<endl;
	}
	else{
		for(char x:ans){
			cout<<x;
		}
		cout<<endl;
	}
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	
	cin>>n;
	for(int i = 0;i < n;i++){
		cin>>s[i];
	}
	
	for(int i = 0;i < n-1;i++){
		int j = 0,k = 0;
		int len1 = s[i].length(),len2 = s[i+1].length();
		//若第一个字母相同，依次比较下一个 
		while(s[i][j] == s[i+1][k]){
			j++;
			k++;
		}
		if(j == len1)
		continue;
		if(k == len2){
			cout<<"Impossible"<<endl;
			return 0;
		}
		g[s[i][j]-'a'].push_back(s[i+1][k]-'a');
		
	}
	
	for(int i = 0;i < 26;i++){
		for(int x:g[i]){
			index[x]++;
		}
	}
	bfs();
	return 0;
}



```
