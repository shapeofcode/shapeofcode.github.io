---
layout: post
title:  "LeetCode - Design Circular Queue"
date:   2021-07-20
last_modified_at: 2021-07-20
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Queue

<br/>

문제 설명 간략 :    

FIFO 구조의 순환 queue를 작성하라. 


<br/>

제약사항

- 1 <= k <= 1000
- 0 <= value <= 1000
- At most 3000 calls will be made to enQueue, deQueue, Front, Rear, isEmpty, and isFull.

<br/>
   

<br/>

### 자바 풀이

```java
class MyCircularQueue {

    int [] queue = null;
    int head = -1;
    int tail = -1;
    int size = 0;

    public MyCircularQueue(int k) {
        queue = new int[k];
        size = k;
    }

    public boolean enQueue(int value) {
        if(isFull()) {
            return false;
        }
        if(isEmpty()) {
            head = 0;
        }

        tail = (tail+1)%size;
        queue[tail] = value;
        return true;
    }

    public boolean deQueue() {
        if(isEmpty()) {
            return false;
        }
        if(head == tail) {
            head = -1;
            tail = -1;
            return true;
        }

        head = (head+1)%size;

        return true;
    }

    public int Front() {
        if(isEmpty()) {
            return -1;
        }
        return queue[head];
    }

    public int Rear() {
        if(isEmpty()) {
            return -1;
        }
        return queue[tail];
    }

    public boolean isEmpty() {
        if(tail == -1) {
            return true;
        }
        return false;
    }

    public boolean isFull() {
        if((tail+1)%size == head) {
            return true;
        }
        return false;
    }
}

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue obj = new MyCircularQueue(k);
 * boolean param_1 = obj.enQueue(value);
 * boolean param_2 = obj.deQueue();
 * int param_3 = obj.Front();
 * int param_4 = obj.Rear();
 * boolean param_5 = obj.isEmpty();
 * boolean param_6 = obj.isFull();
 */


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/228/first-in-first-out-data-structure/1337/)