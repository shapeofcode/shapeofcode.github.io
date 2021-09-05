---
layout: post
title:  "HackerRank - Compare two linked lists"
date:   2021-06-22
last_modified_at: 2021-06-22
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Linked Lists

<br/>

문제 설명 간략 :    

두 Linked List를 비교하여 요소가 모두같고 길이도 같으면 return 1 아니면 return 0. 


<br/>

제약사항

- 1 <= t <= 10
- 1 <= n,m <= 1000
- 1 <= list[i] <= 1000, where list[i] is the i<sup>th</sup> element of the linked list

<br/>
   

<br/>

### 자바 풀이

```java
import java.io.*;
import java.math.*;
import java.text.*;
import java.util.*;
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

    // Complete the compareLists function below.

    /*
     * For your reference:
     *
     * SinglyLinkedListNode {
     *     int data;
     *     SinglyLinkedListNode next;
     * }
     *
     */
    static boolean compareLists(SinglyLinkedListNode head1, SinglyLinkedListNode head2) {

        boolean equal = true;

        try {
            while(head1 != null) {
                if(head1.data != head2.data) {
                    equal = false;
                    break;
                }
                head1 = head1.next;
                head2 = head2.next;
            }
        } catch (Exception e) {
            equal = false;
        }

        return equal;
    }

    private static final Scanner scanner = new Scanner(System.in);


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/compare-two-linked-lists/problem)