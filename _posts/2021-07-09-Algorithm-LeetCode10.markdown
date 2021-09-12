---
layout: post
title:  "LeetCode - Array Partition"
date:   2021-07-09
last_modified_at: 2021-07-09
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

Integer 배열이 주어지고 두개의 조합으로 나오는 최솟값의 합을 구하여라. 


<br/>

제약사항

- 1 <= n <= 10^4
- nums.length == 2 * n
- -10^4 <= nums[i] <= 10^4

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);

        int sum = 0;
        for(int i = 0; i < nums.length-1; i+=2) {
            sum += nums[i];
        }

        return sum;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/205/array-two-pointer-technique/1154/)