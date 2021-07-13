---
layout: post
title:  "HackerRank - Queues: A Tale of Two Stacks"
date:   2021-05-22
last_modified_at: 2021-05-22
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Stacks and Queues

<br/>

문제 설명 간략 :    

두개의 stack을 이용하여 Queue를 완성하여라.

q queries가 주어지고 3가지 type 이 잇다.

1. 1 x: queue의 끝에 x를 넣는다.
2. 2: queue의 앞에 있는 원소를 뺀다.
3. 3: queue의 앞에 있는 원소를 출력한다.

<br/>

제약사항

- 1 <= q <= 10^5
- 1 <= type <= 3
- 1 <= |x| <= 10^9
- type2와 3에 항상 올바른 답이 보장된다.

<br/>

idea 

1. 두개의 stack을 선언하여 enqueue는 new stack에 값을 넣는다.
2. peek은 new stack에서 값을 빼서 old stack에 값을 넣은 후 old stack에서 peek을 한다.
3. dequeue는 2번과 마찬가지로 값을 넣은 후 old stack에서 pop을 한다.

   

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;
import java.text.*;
import java.math.*;
import java.util.regex.*;

public class Solution {
    public static void main(String[] args) {
        MyQueue<Integer> queue = new MyQueue<Integer>();

        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();

        for (int i = 0; i < n; i++) {
            int operation = scan.nextInt();
            if (operation == 1) { // enqueue
                queue.enqueue(scan.nextInt());
            } else if (operation == 2) { // dequeue
                queue.dequeue();
            } else if (operation == 3) { // print/peek
                System.out.println(queue.peek());
            }
        }
        scan.close();
    }
}

class MyQueue<T> {

    Stack<T> oldStack = new Stack<T>();
    Stack<T> newStack = new Stack<T>();

    public void enqueue(T value) {
        newStack.push(value);
    }

    public T peek() {
        if(oldStack.isEmpty()) {
            while(!newStack.isEmpty()) {
                oldStack.push(newStack.pop());
            }
        }

        return oldStack.peek();
    }

    public T dequeue() {
        if(oldStack.isEmpty()) {
            while(!newStack.isEmpty()) {
                oldStack.push(newStack.pop());
            }
        }

        return oldStack.pop();
    }

}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/ctci-queue-using-two-stacks/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=stacks-queues)