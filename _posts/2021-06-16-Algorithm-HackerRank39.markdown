---
layout: post
title:  "HackerRank - Postorder Traversal"
date:   2021-06-16
last_modified_at: 2021-06-16
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Tree

<br/>

문제 설명 간략 :    

후위 순회로 binary tree를 출력하라. 

후위 순회 (LEFT - RIGHT - ROOT)

<br/>

제약사항

- 1 <= Nodes in the tree <= 500

<br/>
   

<br/>

### 자바 풀이

```java


/* you only have to complete the function given below.  
Node is defined as  

class Node {
    int data;
    Node left;
    Node right;
}

*/

public static void postOrder(Node root) {
    if(root == null) {
        return;
    }
    
    postOrder(root.left);
    postOrder(root.right);
    System.out.print(root.data+" ");
    
}




```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/tree-postorder-traversal/problem)