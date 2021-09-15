---
layout: post
title:  "LeetCode - Pascal's Triangle II"
date:   2021-07-15
last_modified_at: 2021-07-15
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Data Structures - String

<br/>

문제 설명 간략 :    

Pascal's triangle에서 rowIndex의 row를 return 하여라. 


<br/>

제약사항

- 0 <= rowIndex <= 33

<br/>
   

<br/>

### 자바 풀이

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {

        List<Integer> resultList = new ArrayList<Integer>();

        resultList.add(1);

        for(int i = 1; i <= rowIndex; i++) {
            for(int j = resultList.size()-2; j >=0; j--) {
                resultList.set(j+1, resultList.get(j)+resultList.get(j+1));
            }
            resultList.add(1);
        }

        return resultList;
    }
}

```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/array-and-string/204/conclusion/1171/)