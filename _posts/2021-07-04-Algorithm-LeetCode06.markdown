---
layout: post
title:  "LeetCode - Pascal's Triangle"
date:   2021-07-04
last_modified_at: 2021-07-04
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - Array

<br/>

문제 설명 간략 :    

integer가 주어지고 Pascal's triangle에 해당하는 원소들을 출력하라. 


<br/>

제약사항

- 1 <= numRows <= 30

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {

        List<List<Integer>> returnList = new ArrayList<List<Integer>>();

        List<Integer> first = new ArrayList<Integer>();
        first.add(1);
        returnList.add(first);

        if(numRows == 1) {
            return returnList;
        }

        List<Integer> second = new ArrayList<Integer>();
        second.add(1);
        second.add(1);
        returnList.add(second);

        if(numRows == 2) {
            return returnList;
        }

        for(int i = 2; i < numRows; i++) {
            List<Integer> subList = new ArrayList<Integer>();
            List<Integer> prevList = returnList.get(i-1);

            subList.add(1);
            for(int j = 0; j < prevList.size()-1; j++) {
                subList.add(prevList.get(j)+prevList.get(j+1));
            }
            subList.add(1);

            returnList.add(subList);
        }

        return returnList;
    }
}


```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/202/introduction-to-2d-array/1170/)