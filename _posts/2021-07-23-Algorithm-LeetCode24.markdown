---
layout: post
title:  "LeetCode - Perfect Squares"
date:   2021-07-23
last_modified_at: 2021-07-23
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Queue and BFS

<br/>

문제 설명 간략 :    

integer n이 주어지고 제곱의 합이 n과 같아지는 최솟값을 구하여라. 


<br/>

제약사항

- 1 <= n <= 104^

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int numSquares(int n) {

        int[] memo = new int[n+1];
        Arrays.fill(memo, Integer.MAX_VALUE);
        memo[0] = 0;

        for(int i = 1; i <= n; i++) {
            for(int j = 1; j*j <= i; j++) {
                memo[i] = Math.min(memo[i-j*j]+1, memo[i]);
            }
        }

        return memo[n];

    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/231/practical-application-queue/1371/)