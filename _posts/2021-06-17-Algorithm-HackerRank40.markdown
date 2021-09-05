---
layout: post
title:  "HackerRank - Inorder Traversal"
date:   2021-06-17
last_modified_at: 2021-06-17
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Tree

<br/>

문제 설명 간략 :    

중위 순회로 binary tree를 출력하라. 

중위 순회(LEFT - ROOT - RIGHT)


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

public static void inOrder(Node root){
    if(root==null){
        return;
    }
    inOrder(root.left);
    System.out.print(root.data+" ");
    inOrder(root.right);
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/tree-inorder-traversal/problem)