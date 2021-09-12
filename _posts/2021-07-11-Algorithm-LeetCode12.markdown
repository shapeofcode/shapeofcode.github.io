---
layout: post
title:  "LeetCode - Remove Element"
date:   2021-07-11
last_modified_at: 2021-07-11
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

Integer 배열이 주어지고 원소가 주어진다. 원소를 제거한 배열을 반환하라.


<br/>

제약사항

- 0 <= nums.length <= 100
- 0 <= nums[i] <= 50
- 0 <= val <= 100

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int removeElement(int[] nums, int val) {

        int k = 0;

        for(int i = 0; i < nums.length; i++) {
            if(nums[i] != val) {
                nums[k] = nums[i];
                k++;
            }
        }

        return k;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/205/array-two-pointer-technique/1151/)