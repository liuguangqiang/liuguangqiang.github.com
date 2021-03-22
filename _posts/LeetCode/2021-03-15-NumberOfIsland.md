---
layout : post 
category : LeetCode
desc : ''
title : Number of Islands
subtitle : 计算岛屿的数量
catalog: true
author: "Eric"
tags:
   - LeetCode
   - Java
   - Python
---


## Number of Islands

### 题目介绍
https://leetcode.com/problems/number-of-islands/description/

Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.
An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. 
You may assume all four edges of the grid are all surrounded by water.

给定一个大小为m*n的二维网格, 假设这是一片水域，且1表示陆地，0表示水， 计算岛屿的数量；
水平和垂直方向连在一起，且并且被水包围的，就是一个岛屿；
您可以假设网格的所有四个边缘都被水包围。

### 例子1:
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

### 例子2:
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

## 思路
* 遍历网格，如果发现值为1的点, 比如grid[0][0]，即表示发现了一个岛屿；
* 然后从这个点开始往垂直和水平方向蔓延开去；
* 如果发现值为1，表示还在这个岛屿范围内，那么继续蔓延检查，并且把这个点标记为0；
* 如果发现值为0，则是出岛屿的边界；
* 经过上面的检查和蔓延， 就可以拿到一个完整的岛屿；
* 当遍历完整个网络后， 就可以统计出这片水域的所有岛屿的数量了；

### java
```java
    public int numIslands(char[][] grid) {
        int count = 0;
        int height = grid.length;
        if (height > 0) {
            int width = grid[0].length;
            for (int h = 0; h < height; h++) {
                for (int w = 0; w < width; w++) {
                    if (grid[h][w] == '1') {
                        count++;
                        floodFill(grid, h, w);
                    }
                }
            }
        }
        return count;
    }

    public void floodFill(char[][] grid, int h, int w) {
        if (h >= 0 && h < grid.length && w >= 0 && w < grid[0].length) {
            int value = grid[h][w];
            if (value == '1') {
                grid[h][w] = '0';
                floodFill(grid, h + 1, w);
                floodFill(grid, h, w + 1);
                floodFill(grid, h - 1, w);
                floodFill(grid, h, w - 1);
            }
        }
    }    
```

