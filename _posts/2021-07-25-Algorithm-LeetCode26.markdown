---
layout: post
title:  "LeetCode - Min Stack"
date:   2021-07-25
last_modified_at: 2021-07-25
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

push, pop, top 그리고 최소값을 반환하는 stack을 구현하라. 


<br/>

제약사항

- -2^31 <= val <= 2^31 - 1
- Methods pop, top and getMin operations will always be called on non-empty stacks.
- At most 3 * 10^4 calls will be made to push, pop, top, and getMin.

<br/>
   

<br/>

### 자바 풀이

```java
class MinStack {

    List<Integer> data = null;

    /** initialize your data structure here. */
    public MinStack() {
        data = new ArrayList<Integer>();
    }

    public void push(int val) {
        data.add(val);
    }

    public void pop() {
        if(data.size() > 0) {
            data.remove(data.size()-1);
        }
    }

    public int top() {
        return data.get(data.size()-1);
    }

    public int getMin() {
        int min = Integer.MAX_VALUE;
        for(int i = 0; i < data.size(); i++) {
            int val = data.get(i);
            if(val  < min) {
                min = val;
            }
        }

        return min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/230/usage-stack/1360/)