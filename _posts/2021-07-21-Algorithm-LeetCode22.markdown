---
layout: post
title:  "LeetCode - Number of Islands"
date:   2021-07-21
last_modified_at: 2021-07-21
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Queue

<br/>

문제 설명 간략 :    

m x n 2d binary grid가 주어지고 1은 땅 0은 물을 나타낸다. 땅의 갯수를 구하여라(물로 둘러 쌓인 덩어리를 땅으로 간주한다.) 


<br/>

제약사항

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 300
- grid[i][j] is '0' or '1'.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int numIslands(char[][] grid) {
        int islands = 0;

        for(int i = 0; i < grid.length; i++) {
            for(int j = 0; j < grid[0].length; j++) {
                if(grid[i][j] == '1') {
                    visit(grid, i, j);
                    islands++;
                }
            }
        }

        return islands;
    }


    public void visit(char[][] grid, int row, int col) {
        grid[row][col] = '-';

        //상
        if(row < grid.length-1 && grid[row+1][col] == '1') {
            visit(grid,row+1,col);
        }

        //하
        if(row > 0 && grid[row-1][col] == '1') {
            visit(grid,row-1,col);
        }

        //좌
        if(col < grid[0].length-1 && grid[row][col+1] == '1') {
            visit(grid,row,col+1);
        }

        //우
        if(col > 0 && grid[row][col-1] == '1') {
            visit(grid,row,col-1);
        }
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/231/practical-application-queue/1374/)