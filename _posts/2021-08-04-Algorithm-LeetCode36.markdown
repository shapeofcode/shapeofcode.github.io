---
layout: post
title:  "LeetCode - Flood Fill"
date:   2021-08-04
last_modified_at: 2021-08-04
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

m x n integer grid가 주어지고 image[i][j]는 image의 pixel value를 의미한다. sr, sc, newColor가 주어지고 
4방향으로 시작지점과 같은 컬러는 새로운 컬러로 대체한다. 


<br/>

제약사항

- m == image.length
- n == image[i].length
- 1 <= m, n <= 50
- 0 <= image[i][j], newColor < 216
- 0 <= sr < m
- 0 <= sc < n

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        int memory[][] = new int[image.length][image[0].length];
        explore(image, memory, image[sr][sc], sr, sc, newColor);
        return image;
    }

    public void explore(int[][] image, int[][] memory, int target, int x, int y, int newColor) {
        if(x < 0 || y < 0 || x >= image.length || y >= image[x].length) {
            return;
        }

        if(memory[x][y] == 1) {
            return;
        }

        if(image[x][y] != target) {
            memory[x][y] = 1;
            return;
        }

        if(image[x][y] == target) {
            memory[x][y] = 1;
            image[x][y] = newColor;

            explore(image, memory, target, x-1, y, newColor);
            explore(image, memory, target, x, y-1, newColor);
            explore(image, memory, target, x+1, y, newColor);
            explore(image, memory, target, x, y+1, newColor);

        }
    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/239/conclusion/1393/)