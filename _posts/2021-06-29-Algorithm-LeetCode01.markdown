---
layout: post
title:  "LeetCode - Find Pivot Index"
date:   2021-06-29
last_modified_at: 2021-06-29
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Array

<br/>

문제 설명 간략 :    

array가 주어지고 왼쪽과 오른쪽 합이 같아지는 index를 찾아라. 


<br/>

제약사항

- 1 <= nums.length <= 10^4
- -1000 <= nums[i] <= 1000

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int pivotIndex(int[] nums) {

        int totalSum = 0;
        int [] sumArray = new int[nums.length];
        int pivotIndex = -1;

        for(int i = 0; i < nums.length; i++) {
            totalSum += nums[i];
            sumArray[i] = totalSum;
        }

        for(int j = 0; j < sumArray.length; j++) {
            if(sumArray[j] - nums[j] == sumArray[sumArray.length-1] - sumArray[j]) {
                return j;
            }
        }

        return pivotIndex;

    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/problems/find-pivot-index/)