---
layout: post
title:  "LeetCode - Implement strStr()"
date:   2021-07-05
last_modified_at: 2021-07-05
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

문자열이 주어지고 부분 문자열이 주어진다. 포함되어 있으면 시작 위치를 출력하고 없으면 -1을 출력하라. 


<br/>

제약사항

- 0 <= haystack.length, needle.length <= 5 * 104
- haystack and needle consist of only lower-case English characters.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int strStr(String haystack, String needle) {

        if(haystack.equals(needle)) {
            return 0;
        }

        int idx = -1;
        int nl = needle.length();
        for(int i = 0; i < haystack.length()-nl+1; i++) {
            if(haystack.substring(i,nl+i).equals(needle)) {
                idx = i;
                break;
            }
        }

        return idx;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/203/introduction-to-string/1161/)