---
layout: post
title:  "LeetCode - Remove Duplicates from Sorted Array"
date:   2021-07-18
last_modified_at: 2021-07-18
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

오름차순으로 정렬된 integer 배열의 중복을 제거하라. 


<br/>

제약사항

- 0 <= nums.length <= 3 * 104
- -100 <= nums[i] <= 100
- nums is sorted in non-decreasing order.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int removeDuplicates(int[] nums) {

        int index = 1;

        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] != nums[i + 1]) {
                nums[index++] = nums[i + 1];
            }
        }

        return index;

    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/204/conclusion/1173/)