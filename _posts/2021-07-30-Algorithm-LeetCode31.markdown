---
layout: post
title:  "LeetCode - Clone Graph"
date:   2021-07-30
last_modified_at: 2021-07-30
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Stack

<br/>

문제 설명 간략 :    

무방향성 graph가 주어지고 deep copy를 반환 하라. 


<br/>

제약사항

- The number of nodes in the graph is in the range [0, 100].
- 1 <= Node.val <= 100
- Node.val is unique for each node.
- There are no repeated edges and no self-loops in the graph.
- The Graph is connected and all nodes can be visited starting from the given node.

<br/>
   

<br/>

### 자바 풀이

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    public Node cloneGraph(Node node) {

        if(node == null) {
            return null;
        }

        Node newNode = new Node(node.val);
        HashMap<Integer, Node> map = new HashMap<>();
        map.put(newNode.val, newNode);

        Queue<Node> q = new LinkedList<>();
        q.add(node);

        while(!q.isEmpty()) {
            Node cur = q.poll();

            for(Node neighbor : cur.neighbors) {
                if(!map.containsKey(neighbor.val)) {
                    map.put(neighbor.val, new Node(neighbor.val));
                    q.add(neighbor);
                }

                map.get(cur.val).neighbors.add(map.get(neighbor.val));
            }
        }

        return newNode;

    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/232/practical-application-stack/1392/)