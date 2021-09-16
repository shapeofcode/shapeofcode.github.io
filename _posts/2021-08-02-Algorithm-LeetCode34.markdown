---
layout: post
title:  "LeetCode - Implement Queue using Stacks"
date:   2021-08-02
last_modified_at: 2021-08-02
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

두개의 stack을 이용하여 queue를 구현하라. 


<br/>

제약사항

- 1 <= x <= 9
- At most 100 calls will be made to push, pop, peek, and empty.
- All the calls to pop and peek are valid.

<br/>
   

<br/>

### 자바 풀이

```java
class MyStack {

    Queue<Integer> q1 = null;
    Queue<Integer> q2 = null;


    /** Initialize your data structure here. */
    public MyStack() {
        q1 = new LinkedList<>();
        q2 = new LinkedList<>();
    }

    /** Push element x onto stack. */
    public void push(int x) {
        if(q1.isEmpty()) {
            q1.add(x);
            while(!q2.isEmpty()) {
                q1.add(q2.poll());
            }
        } else if(q2.isEmpty()) {
            q2.add(x);
            while(!q1.isEmpty()) {
                q2.add(q1.poll());
            }
        }
    }

    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        if(q1.isEmpty()) {
            return q2.poll();
        } else {
            return q1.poll();
        }
    }

    /** Get the top element. */
    public int top() {
        if(q1.isEmpty()) {
            return q2.peek();
        } else {
            return q1.peek();
        }
    }

    /** Returns whether the stack is empty. */
    public boolean empty() {
        return q1.isEmpty() && q2.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/239/conclusion/1386/)