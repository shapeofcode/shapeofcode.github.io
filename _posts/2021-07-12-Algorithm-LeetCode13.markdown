---
layout: post
title:  "LeetCode - Max Consecutive Ones"
date:   2021-07-12
last_modified_at: 2021-07-12
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

연속된 1의 최대 갯수를 구하여라. 


<br/>

제약사항

- 1 <= nums.length <= 10^5
- nums[i] is either 0 or 1.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {

        int maxCount = 0;
        int count = 0;

        for(int i = 0; i < nums.length; i++) {
            if(nums[i] == 0) {
                if(count > maxCount) {
                    maxCount = count;
                }
                count = 0;
            }else{
                count++;
            }
        }

        if(count > maxCount) {
            maxCount = count;
        }

        return maxCount;

    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/205/array-two-pointer-technique/1301/)