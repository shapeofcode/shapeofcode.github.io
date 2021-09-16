---
layout: post
title:  "LeetCode - Move Zeroes"
date:   2021-07-19
last_modified_at: 2021-07-19
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

integer 배열이 주어지고 모든 0을 끝쪽으로 이동 시켜라. 


<br/>

제약사항

- 1 <= nums.length <= 10^4
- -2^31 <= nums[i] <= 2^31 - 1

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public void moveZeroes(int[] nums) {

        int idx = 0;
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] != 0) {
                nums[idx] = nums[i];
                idx++;
            }
        }
        for(int i = idx; i < nums.length; i++) {
            nums[i] = 0;
        }
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/delete-a-node-from-a-linked-list/problem)