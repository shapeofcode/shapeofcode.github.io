---
layout: post
title:  "LeetCode - Open the Lock"
date:   2021-07-22
last_modified_at: 2021-07-22
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Queue

<br/>

문제 설명 간략 :    

4자리 자물쇠가 주어지고 걸리면 안되는 deadends 배열이 주어진다. deadends를 피해 target 번호까지 맞출 수 있는
최소 횟수를 구하여라.


<br/>

제약사항

- 1 <= deadends.length <= 500
- deadends[i].length == 4
- target.length == 4
- target will not be in the list deadends.
- target and deadends[i] consist of digits only.

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public int openLock(String[] deadends, String target) {

        HashSet<String> dead_ends = new HashSet(Arrays.asList(deadends));

        HashSet<String> visited = new HashSet();
        visited.add("0000");

        Queue<String> queue = new LinkedList();
        queue.offer("0000");

        int level = 0;

        while(!queue.isEmpty()) {
            int size = queue.size();
            while(size > 0) {
                String lock_position = queue.poll();
                if(dead_ends.contains(lock_position)) {
                    size--;
                    continue;
                }
                if(lock_position.equals(target)) {
                    return level;
                }

                StringBuilder sb = new StringBuilder(lock_position);
                for(int i = 0; i < 4; i++) {
                    char current_position = sb.charAt(i);
                    String s1 = sb.substring(0,i)+(current_position == '9' ? 0 : current_position - '0' +1)
                            + sb.substring(i+1);
                    String s2 = sb.substring(0,i)+(current_position == '0' ? 9 : current_position - '0' -1)
                            + sb.substring(i+1);

                    if(!visited.contains(s1) && !dead_ends.contains(s1)) {
                        queue.offer(s1);
                        visited.add(s1);
                    }
                    if(!visited.contains(s2) && !dead_ends.contains(s2)) {
                        queue.offer(s2);
                        visited.add(s2);
                    }
                }

                size--;
            }
            level++;
        }

        return -1;

    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/231/practical-application-queue/1375/)