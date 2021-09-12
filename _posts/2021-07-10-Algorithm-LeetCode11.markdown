---
layout: post
title:  "LeetCode - Two Sum II - Input array is sorted"
date:   2021-07-10
last_modified_at: 2021-07-10
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

오름차순으로 정렬된 integer 배열이 주어지고 두개의 원소의 합이 target과 같아지는 index를 반환하라. 


<br/>

제약사항

- 2 <= numbers.length <= 3 * 10^4
- -1000 <= numbers[i] <= 1000
- numbers is sorted in non-decreasing order.
- -1000 <= target <= 1000
- The tests are generated such that there is exactly one solution.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {

        int [] twoSum = new int[2];

        int nl = numbers.length;

        int endIdx = nl-1;

        for(int j = 0; j < nl; j++) {
            if(numbers[j] > target) {
                endIdx = j;
                break;
            }
        }

        for(int i = 0; i <= endIdx; i++) {
            for(int j = i+1; j <= endIdx; j++) {
                if(target == (numbers[i]+numbers[j])) {
                    twoSum[0] = i+1;
                    twoSum[1] = j+1;
                    break;
                }
            }
        }

        return twoSum;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/205/array-two-pointer-technique/1153/)