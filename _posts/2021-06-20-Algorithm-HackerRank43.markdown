---
layout: post
title:  "HackerRank - Print in Reverse"
date:   2021-06-20
last_modified_at: 2021-06-20
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Linked Lists

<br/>

문제 설명 간략 :    

Singly-linked list를 거꾸로 출력하라.


<br/>

제약사항

- 1 <= n <= 1000
- 1 <= list[i] <= 1000, where list[i] is the i<sup>th</sup> element of the linked list

<br/>
   

<br/>

### 자바 풀이

```java

/*
 * Complete the 'reversePrint' function below.
 *
 * The function accepts INTEGER_SINGLY_LINKED_LIST llist as parameter.
 */

/*
 * For your reference:
 *
 * SinglyLinkedListNode {
 *     int data;
 *     SinglyLinkedListNode next;
 * }
 *
 */

public static void reversePrint(SinglyLinkedListNode llist) {

    if(llist == null) {
        return;
    }

    reversePrint(llist.next);
    System.out.println(llist.data);

}




```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/print-the-elements-of-a-linked-list-in-reverse/problem)