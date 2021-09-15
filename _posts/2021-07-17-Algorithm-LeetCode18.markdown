---
layout: post
title:  "LeetCode - Reverse Words in a String III"
date:   2021-07-17
last_modified_at: 2021-07-17
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

String s 가 주어지고 모든 알파벳을 거꾸로 출력하라(띄어쓰기 포함). 


<br/>

제약사항

- 1 <= s.length <= 5 * 10^4
- s contains printable ASCII characters. 
- s does not contain any leading or trailing spaces. 
- There is at least one word in s.
- All the words in s are separated by a single space.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public String reverseWords(String s) {

        String[] arr = s.split(" ");

        String blank = "";

        for (String str : arr) {

            if (blank.length() > 0) {
                blank += " ";
            }

            blank += new StringBuilder(str).reverse();
        }

        return blank;

    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/204/conclusion/1165/)