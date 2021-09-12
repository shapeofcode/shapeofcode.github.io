---
layout: post
title:  "LeetCode - Plus One"
date:   2021-07-01
last_modified_at: 2021-07-01
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Array

<br/>

문제 설명 간략 :    

정수를 표현하는 배열이 주어지고 그보다 1이 큰 정수를 표현하는 배열을 반환하라. 


<br/>

제약사항

- 1 <= digits.length <= 100
- 0 <= digits[i] <= 9
- digits does not contain any leading 0's

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int[] plusOne(int[] digits) {

        for(int i = digits.length-1; i >= 0; i--) {

            if(i == digits.length-1) {
                digits[i]++;
            }

            if(i == 0 && digits[i] == 10) {
                int [] plusOne = new int [digits.length+1];
                plusOne[0] = 1;
                digits[i] = 0;
                for(int j = 1; j < plusOne.length; j++) {
                    plusOne[j] = digits[j-1];
                }
                return plusOne;
            }


            if(digits[i] == 10) {
                digits[i] = 0;
                digits[i-1]++;
            }

        }

        return digits;

    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/201/introduction-to-array/1148/)