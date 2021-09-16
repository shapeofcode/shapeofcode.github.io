---
layout: post
title:  "LeetCode - Decode String"
date:   2021-08-03
last_modified_at: 2021-08-03
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

k[encoded_string] 형태의 string이 주어지고 encoded_string을 k번 반복하여 decoded string을 반환하라.


<br/>

제약사항

- 1 <= s.length <= 30
- s consists of lowercase English letters, digits, and square brackets '[]'.
- s is guaranteed to be a valid input.
- All the integers in s are in the range [1, 300].

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public String decodeString(String s) {

        Stack<String> strStack = new Stack<>();
        Stack<Integer> numStack = new Stack<>();
        StringBuilder res = new StringBuilder();
        StringBuilder numSb = new StringBuilder();

        int idx = 0;
        while (idx < s.length()) {
            char curLetter = s.charAt(idx);
            if (Character.isDigit(curLetter)) {
                numSb.append(curLetter);
                idx++;
            } else if (curLetter == '[') {
                numStack.push(Integer.parseInt(numSb.toString()));
                strStack.push(res.toString());
                numSb = new StringBuilder();
                res = new StringBuilder();
                idx++;
            } else if (curLetter == ']') {
                StringBuilder temp = new StringBuilder(strStack.pop());
                int repeatTimes = numStack.pop();
                for (int i = 0; i < repeatTimes; i++) {
                    temp.append(res);
                }
                res = temp;
                idx++;
            } else {
                res.append(s.charAt(idx++));
            }
        }
        return res.toString();
    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/239/conclusion/1379/)