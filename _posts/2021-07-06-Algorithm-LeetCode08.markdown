---
layout: post
title:  "LeetCode - Longest Common Prefix"
date:   2021-07-06
last_modified_at: 2021-07-06
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

string 배열의 공통된 prefix를 출력하라. 


<br/>

제약사항

- 1 <= strs.length <= 200
- 0 <= strs[i].length <= 200
- strs[i] consists of only lower-case English letters.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {

        StringBuilder sb = new StringBuilder();

        boolean hasPrefix = true;

        int shortestLength = 200;

        for(int i = 0; i < strs.length; i++) {
            int sl = strs[i].length();
            if(shortestLength > sl) {
                shortestLength = sl;
            }
        }

        int idx = 0;

        while(hasPrefix && idx < shortestLength) {
            char c = strs[0].charAt(idx);
            for(int j = 1; j < strs.length; j++) {
                if(strs[j].charAt(idx) != c) {
                    hasPrefix = false;
                    break;
                }
            }

            if(hasPrefix) {
                sb.append(c);
                idx++;
            }
        }

        String prefix = sb.toString();
        return prefix;


    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/203/introduction-to-string/1162/)