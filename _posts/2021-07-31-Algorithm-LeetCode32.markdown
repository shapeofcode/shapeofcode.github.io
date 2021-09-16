---
layout: post
title:  "LeetCode - Target Sum"
date:   2021-07-31
last_modified_at: 2021-07-31
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

inteter 배열과 target 값이 주어진다. +,-를 사용해서 target 값을 만드는 방법의 수를 구하여라. 


<br/>

제약사항

- 1 <= nums.length <= 20
- 0 <= nums[i] <= 1000
- 0 <= sum(nums[i]) <= 1000
- -1000 <= target <= 1000

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int[][] memo = new int[nums.length][2001];
        for (int[] row : memo) {
            Arrays.fill(row, Integer.MIN_VALUE);
        }
        return dfs(nums, 0, 0, target, memo);
    }

    private int dfs(int[] nums, int index, int sum, int S, int[][] memo) {
        if(index == nums.length) {
            return S == sum ? 1 : 0;
        }

        if(memo[index][sum+1000] != Integer.MIN_VALUE) {
            return memo[index][sum+1000];
        }

        int add = dfs(nums, index + 1, sum + nums[index], S, memo);
        int subtract = dfs(nums, index + 1, sum - nums[index], S, memo);

        memo[index][sum + 1000] = add + subtract;

        return memo[index][sum + 1000];
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/203/introduction-to-string/1160/)