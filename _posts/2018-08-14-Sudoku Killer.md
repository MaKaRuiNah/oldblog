---
layout:     post
title:      Sudoku Killer
subtitle: Sudoku Killer-dfs
date:       2018-08-14
author:     Manson
header-img: img/gakki3.jpg
catalog: true
tags:
    - hdu
    - dfs
---
[http://acm.hdu.edu.cn/showproblem.php?pid=1426](http://acm.hdu.edu.cn/showproblem.php?pid=1426)

# 问题描述

自从2006年3月10日至11日的首届数独世界锦标赛以后，数独这项游戏越来越受到人们的喜爱和重视。
据说，在2008北京奥运会上，会将数独列为一个单独的项目进行比赛，冠军将有可能获得的一份巨大的奖品———HDU免费七日游外加lcy亲笔签名以及同hdu acm team合影留念的机会。
所以全球人民前仆后继，为了奖品日夜训练茶饭不思。当然也包括初学者linle，不过他太笨了又没有多少耐性，只能做做最最基本的数独题，不过他还是想得到那些奖品，你能帮帮他吗？你只要把答案告诉他就可以，不用教他是怎么做的。

数独游戏的规则是这样的：在一个9x9的方格中，你需要把数字1-9填写到空格当中，并且使方格的每一行和每一列中都包含1-9这九个数字。同时还要保证，空格中用粗线划分成9个3x3的方格也同时包含1-9这九个数字。比如有这样一个题，大家可以仔细观察一下，在这里面每行、每列，以及每个3x3的方格都包含1-9这九个数字。

例题：

![http://acm.hdu.edu.cn/data/images/C31-1001-1.jpg](http://acm.hdu.edu.cn/data/images/C31-1001-1.jpg)

答案：

![http://acm.hdu.edu.cn/data/images/C31-1001-2.jpg](http://acm.hdu.edu.cn/data/images/C31-1001-2.jpg)

**Input**

本题包含多组测试，每组之间由一个空行隔开。每组测试会给你一个 9*9 的矩阵，同一行相邻的两个元素用一个空格分开。其中1-9代表该位置的已经填好的数，问号（?）表示需要你填的数。
 
**Output**

对于每组测试，请输出它的解，同一行相邻的两个数用一个空格分开。两组解之间要一个空行。
对于每组测试数据保证它有且只有一个解。

# 问题分析
> 本题就是一个解数独的问题，直接用dfs即可，在剪枝时要注意剪枝条件，同一行，同一列不能有相同数字，小九宫格也不能有相同数字。这题最坑的一点就是它的输入了。。。
 
# AC代码


```

/*
author:Manson
date:8.14.2018
theme:Sudoku Killer
*/
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N = 1005;

int Map[9][9];
int num;
struct node{
	int x;
	int y;
}a[81];

int judge(int k,int cur){
	//剪枝，在同行或者填列 
	for(int i = 0;i < 9;i++){
		if(Map[i][a[cur].y] == k || Map[a[cur].x][i] == k){
			return 0;
		}
	}
	int x = a[cur].x/3*3;
	int y = a[cur].y/3*3;
	//在小九宫格 
	for(int i = x;i < x+3;i++){
		for(int j = y;j < y+3;j++){
			if(Map[i][j] == k){
				return 0;
			}
		}
	}
	return 1;
}
//cur = ?的数量 
void dfs(int cur){
	int i,j,flag = 0;
	if(cur == num){
		for(i = 0;i < 9;i++){
			for(j = 0;j < 9;j++){
				if(j == 8){
					cout<<Map[i][j]<<endl;
					break;
				}
				cout<<Map[i][j]<<" ";
			}
		}
		flag = 1;
		return;
	}
	//填数 
	for(i = 1;i <= 9;i++){
		if(judge(i,cur) && !flag){
			Map[a[cur].x][a[cur].y] = i;
			dfs(cur+1);
			Map[a[cur].x][a[cur].y] = 0;
		}
	}
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(0);
	num = 0;
	int cnt = 0;
	int i = 0,j = 0;
	char s[3];
	while(cin>>s){
		if(s[0] != '?'){
			Map[i][j] = s[0] - '0';
		}
		else{
			Map[i][j] = 0;
			a[num].x = i;
			a[num].y = j;
			num++;
		}
		j++;
		if(j == 9){
			i++;
			j = 0;
		}
		if(i == 9){
			if(cnt){
				cout<<endl;
			}
			cnt++;
			dfs(0);
			num = i = j = 0; 
		}
	}
	
	return 0;
}


```
