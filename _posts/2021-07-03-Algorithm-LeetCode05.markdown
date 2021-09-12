---
layout: post
title:  "LeetCode - Spiral Matrix"
date:   2021-07-03
last_modified_at: 2021-07-03
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Array

<br/>

문제 설명 간략 :    

m x n matrix가 주어지고 spiral 순서로 출력하라. 


<br/>

제약사항

- m == mat.length
- n == mat[i].length
- 1 <= m, n <= 10
- -100 <= matrix[i][j] <= 10

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {

        int width = matrix[0].length;
        int height = matrix.length;

        List<Integer> result = new ArrayList<Integer>();

        //right -> down -> left -> up

        String direction = "right";

        int idx = -1;
        int x = -1;
        int y = 0;
        int [][] check = new int[height][width];
        while(idx < width*height-1) {
            if(direction.equals("right")) {
                x++;
                if(x == width || check[y][x] == 1) {
                    direction = "down";
                    x--;
                    continue;
                }
            }else if(direction.equals("down")) {
                y++;
                if(y == height || check[y][x] == 1) {
                    direction = "left";
                    y--;
                    continue;
                }
            }else if(direction.equals("left")) {
                x--;
                if(x == -1 || check[y][x] == 1) {
                    direction = "up";
                    x++;
                    continue;
                }
            }else if(direction.equals("up")) {
                y--;
                if(y == -1 || check[y][x] == 1) {
                    direction = "right";
                    y++;
                    continue;
                }
            }

            idx++;
            result.add(matrix[y][x]);
            check[y][x] = 1;

        }

        return result;

    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/202/introduction-to-2d-array/1168/)