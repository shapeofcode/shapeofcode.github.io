---
layout: post
title:  "LeetCode - Reverse Words in a String"
date:   2021-07-16
last_modified_at: 2021-07-16
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

String s가 주어지고 words의 순서를 반대로 출력하라. 


<br/>

제약사항

- 1 <= s.length <= 10^4
- s contains English letters (upper-case and lower-case), digits, and spaces ' '.
- There is at least one word in s.

<br/>
   

<br/>

### 자바 풀이

```java
 class Solution {
    public String reverseWords(String s) {

        List<String> words = new ArrayList<String>();

        StringBuilder returnSb = new StringBuilder();
        StringBuilder sb = new StringBuilder();

        int wordLength = 0;
        for(int i = 0; i < s.length(); i++) {
            if(s.charAt(i) != ' ') {
                sb.append(s.charAt(i));
            }else{
                words.add(sb.toString());
                sb = new StringBuilder();
            }
        }

        words.add(sb.toString());


        for(int k = words.size()-1; k >= 0; k--) {
            if(words.get(k).length() > 0) {
                returnSb.append(words.get(k));
                returnSb.append(" ");
            }
        }

        returnSb.deleteCharAt(returnSb.length()-1);

        return returnSb.toString();
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/204/conclusion/1164/)