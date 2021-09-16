---
layout: post
title:  "LeetCode - Binary Tree Inorder Traversal"
date:   2021-08-01
last_modified_at: 2021-08-01
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

binary tree의 root가 주어지고 중위 순회로 node value를 반환하라. 


<br/>

제약사항

- The number of nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100.

<br/>
   

<br/>

### 자바 풀이

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

    List<Integer> list;

    public List<Integer> inorderTraversal(TreeNode root) {
        list = new ArrayList<Integer>();
        inorder(root);
        return list;
    }

    public void inorder(TreeNode node) {
        if(node != null) {
            if(node.left != null) {
                inorder(node.left);
            }
            list.add(node.val);
            if(node.right != null) {
                inorder(node.right);
            }
        }
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/203/introduction-to-string/1160/)