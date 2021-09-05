---
layout: post
title:  "HackerRank - Preorder Traversal"
date:   2021-06-15
last_modified_at: 2021-06-15
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Tree

<br/>

문제 설명 간략 :    

전위 순회로 binary tree를 출력하라

전위 순회 (ROOT - LEFT - RIGHT)


<br/>

제약사항

- 1 <= Nodes in the tree <= 500

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

public static void preOrder(Node root) {

    if(root==null){
        return;
    }

    System.out.print(root.data+" ");
    preOrder(root.left);
    preOrder(root.right);

}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/tree-preorder-traversal/problem)