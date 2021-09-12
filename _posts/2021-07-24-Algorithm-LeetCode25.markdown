---
layout: post
title:  "LeetCode - Add Binary"
date:   2021-07-24
last_modified_at: 2021-07-24
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

두개의 binary string이 주어지고 둘의 binary string 합을 출력하라. 


<br/>

제약사항

- 1 <= a.length, b.length <= 10000
- a and b consist only of '0' or '1' characters.
- Each string does not contain leading zeros except for the zero itself.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public String addBinary(String a, String b) {
        String result = "";

        int s = 0;

        int i = a.length()-1;
        int j = b.length()-1;

        while(i >= 0 || j >= 0 || s ==1) {
            s += ((i >= 0)? a.charAt(i) - '0' : 0);
            s += ((j >= 0)? b.charAt(j) - '0' : 0);

            result = (char)(s % 2 + '0') + result;

            s = s/2;

            i--; j--;
        }

        return result;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/203/introduction-to-string/1160/)