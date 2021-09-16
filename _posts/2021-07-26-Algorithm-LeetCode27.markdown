---
layout: post
title:  "LeetCode - Valid Parentheses"
date:   2021-07-26
last_modified_at: 2021-07-26
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

'(', ')', '{', '}', '[' and ']' 으로 구성된 String s가 주어지고 열고 닫느게 유효한지 구하여라.


<br/>

제약사항

- 1 <= s.length <= 10^4 
- s consists of parentheses only '()[]{}'.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        Map<Character,Character> pair = new HashMap<Character,Character>();
        pair.put(']','[');
        pair.put('}','{');
        pair.put(')','(');

        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if(stack.empty()) {
                stack.push(c);
            }else{
                char top = stack.peek();
                if(pair.get(c) != null && top == pair.get(c)) {
                    stack.pop();
                } else {
                    stack.push(c);
                }
            }
        }

        boolean valid = false;
        if(stack.empty()) {
            valid = true;
        }

        return valid;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/230/usage-stack/1361/)