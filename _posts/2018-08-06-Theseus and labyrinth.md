---
layout:     post
title:      Theseus and labyrinth
subtitle: Theseus and labyrinth-bfs问题
date:       2018-08-06
author:     Manson
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - codeforces
    - bfs
---
[https://codeforces.com/contest/676/problem/D](https://codeforces.com/contest/676/problem/D)

# 问题描述
Theseus has just arrived to Crete to fight Minotaur. He found a labyrinth that has a form of a rectangular field of size n × m and consists of blocks of size 1 × 1.
Each block of the labyrinth has a button that rotates all blocks 90 degrees clockwise. Each block rotates around its center and doesn’t change its position in the labyrinth. Also, each block has some number of doors (possibly none). In one minute, Theseus can either push the button in order to rotate all the blocks 90 degrees clockwise or pass to the neighbouring block. Theseus can go from block A to some neighbouring block B only if block A has a door that leads to block B and block B has a door that leads to block A.
Theseus found an entrance to labyrinth and is now located in block (xT, yT) — the block in the row xT and column yT. Theseus know that the Minotaur is hiding in block (xM, yM) and wants to know the minimum number of minutes required to get there.
Theseus is a hero, not a programmer, so he asks you to help him.

**Input**

The first line of the input contains two integers n and m (1 ≤ n, m ≤ 1000) the number of rows and the number of columns in labyrinth, respectively.
Each of the following n lines contains m characters, describing the blocks of the labyrinth. The possible characters are:

«+» means this block has 4 doors (one door to each neighbouring block);
«-» means this block has 2 doors -to the left and to the right neighbours;
«|» means this block has 2 doors - to the top and to the bottom neighbours;
«^» means this block has 1 door - to the top neighbour;
«>» means this block has 1 door - to the right neighbour;
«<» means this block has 1 door - to the left neighbour;
«v» means this block has 1 door - to the bottom neighbour;
«L» means this block has 3 doors - to all neighbours except left one;
«R» means this block has 3 doors - to all neighbours except right one;
«U» means this block has 3 doors - to all neighbours except top one;
«D» means this block has 3 doors - to all neighbours except bottom one;
«*» means this block is a wall and has no doors.



# 问题分析
>问题大意是 主人公从一个起点走到一个终点。每一个点的四周有门或墙，只有两个们相对是才能走通。当然也可以停下一秒，使得所有的门都旋转90°。问从起点到达终点所需要的最短路径。
>这里我们可以用g[x][y],表示点(x,y)的可走方向。used[x][y][5]表示方向是否走过。然后用bfs可以模拟过程，求出所需的最短时间。
