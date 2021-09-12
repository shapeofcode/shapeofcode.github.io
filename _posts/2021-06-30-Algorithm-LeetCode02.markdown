---
layout: post
title:  "LeetCode - Largest Number At Least Twice of Others"
date:   2021-06-30
last_modified_at: 2021-06-30
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Array

<br/>

문제 설명 간략 :    

배열이 주어지고 다른 원소들보다 최소 2배 이상 큰 원소를 찾아라. 


<br/>

제약사항

- 1 <= nums.length <= 50
- 0 <= nums[i] <= 100
- The largest element in nums is unique.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int dominantIndex(int[] nums) {

        int dominantIndex = -1;

        if(nums.length == 1) {
            return 0;
        }

        int maxInt = Integer.MIN_VALUE;

        for(int i = 0 ; i <  nums.length; i++) {
            if(maxInt < nums[i]) {
                maxInt = nums[i];
                dominantIndex = i;
            }
        }

        for(int j = 0 ; j <  nums.length; j++) {
            if(dominantIndex == j) {
                continue;
            }
            if(maxInt < nums[j]*2) {
                dominantIndex = -1;
                break;
            }
        }

        return dominantIndex;

    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/problems/largest-number-at-least-twice-of-others/)