---
layout: post
title:  "HackerRank - Binary Search Tree:Insertion"
date:   2021-06-19
last_modified_at: 2021-06-19
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Trees

<br/>

문제 설명 간략 :    

binary search tree에 특정 위치에 값을 넣고 tree의 root를 반환하여라.


<br/>

제약사항

- No. of nodes in the tree <= 500

<br/>
   

<br/>

### 자바 풀이

```java


/* Node is defined as :
class Node 
   int data;
   Node left;
   Node right;
   
   */

public static Node insert(Node root,int data) {

    if(root==null) {
        Node node = new Node(data);
        root = node;
    } else if(root.data > data) {
        root.left = insert(root.left, data);
    } else if(root.data < data) {
        root.right = insert(root.right, data);
    }

    return root;
}

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/binary-search-tree-insertion/problem)