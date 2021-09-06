---
layout: post
title:  "HackerRank - Queue using Two Stacks"
date:   2021-06-26
last_modified_at: 2021-06-26
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Queues

<br/>

문제 설명 간략 :    

두개의 stack을 이용하여 Queue(FIFO)를 구현하라.

1 x: Enqueue element  into the end of the queue.

2: Dequeue the element at the front of the queue.

3: Print the element at the front of the queue.


<br/>

제약사항

- 1 <= q <= 10^5
- 1 <= type <= 3
- 1 <= |x| <= 10^9

<br/>
   

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int quries = in.nextInt();

        Stack<Integer> one = new Stack<Integer>();
        Stack<Integer> two = new Stack<Integer>();

        int query;

        for(int i = 0; i < quries; i++) {
            query = in.nextInt();

            if(query == 1) {
                one.push(in.nextInt());
            }else if(query == 2) {
                if(two.isEmpty()){
                    while(!one.isEmpty()) {
                        two.push(one.pop());
                    }
                }

                if(!two.isEmpty()){
                    two.pop();
                }
            }else if(query == 3) {
                if(two.isEmpty()) {
                    while(!one.isEmpty()) {
                        two.push(one.pop());
                    }
                    System.out.println(two.peek());
                }else {
                    System.out.println(two.peek());
                }
            }
        }
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/queue-using-two-stacks/problem)