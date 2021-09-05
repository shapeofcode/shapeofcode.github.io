---
layout: post
title:  "HackerRank - Reverse a linked list"
date:   2021-06-21
last_modified_at: 2021-06-21
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Linked Lists

<br/>

문제 설명 간략 :    

Linked List head node에 포인터가 주어지고 다음 node의 포인터와 바꿔서 거꾸로 바꾸어라.


<br/>

제약사항

- 1 <= ㅅ <= 10
- 1 <= n <= 1000
- 1 <= list[i] <= 1000, where list[i] is the i<sup>th</sup> element of the linked list

<br/>
   

<br/>

### 자바 풀이

```java
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.regex.*;

public class Solution {

    static class SinglyLinkedListNode {
        public int data;
        public SinglyLinkedListNode next;

        public SinglyLinkedListNode(int nodeData) {
            this.data = nodeData;
            this.next = null;
        }
    }

    static class SinglyLinkedList {
        public SinglyLinkedListNode head;
        public SinglyLinkedListNode tail;

        public SinglyLinkedList() {
            this.head = null;
            this.tail = null;
        }

        public void insertNode(int nodeData) {
            SinglyLinkedListNode node = new SinglyLinkedListNode(nodeData);

            if (this.head == null) {
                this.head = node;
            } else {
                this.tail.next = node;
            }

            this.tail = node;
        }
    }

    public static void printSinglyLinkedList(SinglyLinkedListNode node, String sep, BufferedWriter bufferedWriter) throws IOException {
        while (node != null) {
            bufferedWriter.write(String.valueOf(node.data));

            node = node.next;

            if (node != null) {
                bufferedWriter.write(sep);
            }
        }
    }

    /*
     * Complete the 'reverse' function below.
     *
     * The function is expected to return an INTEGER_SINGLY_LINKED_LIST.
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

    public static SinglyLinkedListNode reverse(SinglyLinkedListNode llist) {

        if(llist == null) {
            return null;
        }

        SinglyLinkedListNode prevNode = null;
        SinglyLinkedListNode curNode = llist;
        SinglyLinkedListNode nextNode = null;

        while(curNode != null) {
            nextNode = curNode.next;
            curNode.next = prevNode;
            prevNode = curNode;
            curNode = nextNode;
        }

        llist = prevNode;

        return llist;

    }

private static final Scanner scanner = new Scanner(System.in);


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/reverse-a-linked-list/problem)