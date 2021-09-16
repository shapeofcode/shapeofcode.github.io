---
layout: post
title:  "LeetCode - Evaluate Reverse Polish Notation"
date:   2021-07-28
last_modified_at: 2021-07-28
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

+, -, *, / operators가 주어지고 두 integer 사이에 operator가 나오면 순차적으로 실행하여 결과값을 출력하라.


<br/>

제약사항

- 1 <= tokens.length <= 104
- tokens[i] is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int evalRPN(String[] tokens) {
        List<String> operators = new ArrayList<String>();
        operators.add("+");
        operators.add("-");
        operators.add("*");
        operators.add("/");

        Stack<String> stack = new Stack<String>();
        for(int i = 0; i < tokens.length; i++) {
            String token = tokens[i];
            if(operators.contains(token)) {
                int top = Integer.parseInt(stack.peek());
                System.out.println("pop "+top);
                stack.pop();
                int forward = Integer.parseInt(stack.peek());
                stack.pop();
                int calVal = calOperator(forward, token, top);
                stack.push(String.valueOf(calVal));
            }else{
                stack.push(token);
            }
        }

        return Integer.parseInt(stack.peek());

    }

    public int calOperator(int temp, String operator, int token) {

        if(operator.equals("+")) {
            temp = temp + token;
        }else if(operator.equals("-")) {
            temp = temp - token;
        }else if(operator.equals("*")) {
            temp = temp * token;
        }else{
            temp = temp / token;
        }

        return temp;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/230/usage-stack/1394/)