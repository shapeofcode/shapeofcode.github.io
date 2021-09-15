---
layout: post
title:  "LeetCode - Rotate Array"
date:   2021-07-14
last_modified_at: 2021-07-14
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

양수 k가 주어지고 배열을 오른쪽으로 k만큼 순환시켜라. 


<br/>

제약사항

- 1 <= nums.length <= 10^5
- -2^31 <= nums[i] <= 2^31 - 1
- 0 <= k <= 10^5

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public void rotate(int[] nums, int k) {

        int nl = nums.length;
        int[] returnArray = new int[nl];

        for(int i = 0; i < nl; i++) {
            returnArray[(i+k)%nl] = nums[i];
        }

        for(int j = 0; j < nl; j++) {
            nums[j] = returnArray[j];
        }

    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/204/conclusion/1182/)