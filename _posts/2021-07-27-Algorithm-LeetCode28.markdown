---
layout: post
title:  "LeetCode - Daily Temperatures"
date:   2021-07-27
last_modified_at: 2021-07-27
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

온도가 담긴 integer 배열이 주어지고 따뜻해지는 날의 갯수를 반환하라. 


<br/>

제약사항

- 1 <= temperatures.length <= 105
- 30 <= temperatures[i] <= 100

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int [] days = new int[temperatures.length];

        Stack<Integer> stack = new Stack<>();

        for(int i = 0; i < temperatures.length; i++) {
            while(!stack.empty() && temperatures[stack.peek()] < temperatures[i]) {
                int idx = stack.pop();
                days[idx] = i - idx;
            }

            stack.push(i);
        }

        return days;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/230/usage-stack/1363/)