---
layout: post
title:  "LeetCode - Reverse String"
date:   2021-07-08
last_modified_at: 2021-07-08
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

추가 메모리를 사용하지 않고 배열의 원소를 reverse로 배치하라. 


<br/>

제약사항

- 1 <= s.length <= 10^5
- s[i] is a printable ascii character.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public void reverseString(char[] s) {
        int middleIdx = s.length/2;

        int f = 0;
        int b = s.length-1;

        while(f < middleIdx) {
            char temp = s[f];
            s[f] = s[b];
            s[b] = temp;

            f++;
            b--;
        }

        for(int i = 0; i < s.length; i++) {
            System.out.print(s[i]);
        }

    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/205/array-two-pointer-technique/1183/)