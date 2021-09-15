---
layout: post
title:  "LeetCode - Minimum Size Subarray Sum"
date:   2021-07-13
last_modified_at: 2021-07-13
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 : 양의 정수 배열이 주어지고 target 값이 주어진다. 가장 짧은 연속된 부분 배열의 합이 target 값과 같아지는 
길이를 반환하라 없으면 0을 반환한다.

<br/>

제약사항

- 1 <= target <= 10^9 
- 1 <= nums.length <= 10^5
- 1 <= nums[i] <= 10^5

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {

        int minSubArrayLen = Integer.MAX_VALUE;


        for(int i = 0; i < nums.length; i++) {
            int temp = 0;
            for(int j = i; j < nums.length; j++) {
                temp += nums[j];
                if(temp >= target) {
                    int length = j-i+1;
                    if(minSubArrayLen > length) {
                        minSubArrayLen = length;
                    }
                }
            }
        }

        if(minSubArrayLen == Integer.MAX_VALUE) {
            minSubArrayLen = 0;
        }

        return minSubArrayLen;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/205/array-two-pointer-technique/1299/)