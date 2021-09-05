---
layout: post
title:  "HackerRank - Level Order Traversal"
date:   2021-06-18
last_modified_at: 2021-06-18
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Tree

<br/>

문제 설명 간략 :    

왼쪽부터 오른쪽으로 레벨 순회로 binary tree의 값을 출력하라.

<br/>

제약사항

- 1 <= Nodes in the tree <= 500

<br/>
   

<br/>

### 자바 풀이

```java


/* 

class Node 
    int data;
    Node left;
    Node right;
*/
public static void levelOrder(Node root) {

    Queue queue = new LinkedList();
    queue.add(root);

    while(!queue.isEmpty()) {

        Node level = (Node) queue.poll();
    
        System.out.print(level.data+" ");
    
        if(level.left!=null){
            queue.add(level.left);
        }
    
        if(level.right!=null){
            queue.add(level.right);
        }

    }
}




```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/tree-level-order-traversal/problem)