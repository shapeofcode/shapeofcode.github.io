---
layout: post
title:  "LeetCode - Diagonal Traverse"
date:   2021-07-02
last_modified_at: 2021-07-02
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Array

<br/>

문제 설명 간략 :    

m x n matrix가 주어지고 diagonal order 순서(우상향, 좌하향 교차 순서)로 출력하라. 


<br/>

제약사항

- m == mat.length
- n == mat[i].length
- 1 <= m, n <= 10^4
- 1 <= m * n <= 10^4
- -10^5 <= mat[i][j] <= 10^5

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int[] findDiagonalOrder(int[][] mat) {

        if (mat == null || mat.length == 0) {
            return new int[0];
        }

        int height = mat.length;
        int width = mat[0].length;

        int[] result = new int[height*width];
        int k = 0;
        ArrayList<Integer> intermediate = new ArrayList<Integer>();

        for(int i = 0; i < height+width-1; i++) {
            intermediate.clear();

            int r = i < width ? 0 : i - width + 1;
            int c = i < width ? i : width - 1;

            while(r < height && c > -1) {
                intermediate.add(mat[r][c]);
                ++r;
                --c;
            }

            if(i%2 == 0) {
                Collections.reverse(intermediate);
            }

            for(int j = 0; j < intermediate.size(); j++) {
                result[k++] = intermediate.get(j);
            }
        }

        return result;
    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/202/introduction-to-2d-array/1167/)