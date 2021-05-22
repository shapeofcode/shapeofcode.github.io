---
layout: post
title:  "HackerRank - Candies"
date:   2021-04-27
last_modified_at: 2021-04-27
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Greedy

<br/>

문제 설명 간략 : 엘리스는 유치원 선생님이고 최소한 사탕 1개씩 아이들에게 주고 싶고 점수가 높은 아이에게는
하나 더 주고 싶다. 총 엘리스가 주어야할 사탕의 최소 개수를 구하여라.

<br/>

제약사항

- 1 <= n <= 10^5
- 1 <= arr[i] <= 10^5

<br/>

idea 

1. 루프를 돌면서 이전 값보다 현재 값이 크면 이전 값에 +1 아닌 경우 일단 1을 배정. (왼쪽의 큰 값에 대한 만족)
2. 거꾸로 루프를 돌면서 이전 값이 현재 값보다 크면 이전 사탕 개수는 현재 사탕 개수보다 하나 더 배정. (오른쪽의 큰 값에 대한 만족)

<br/>

### 자바 풀이

```java
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;

class Result {

    /*
     * Complete the 'candies' function below.
     *
     * The function is expected to return a LONG_INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER n
     *  2. INTEGER_ARRAY arr
     */

    public static long candies(int n, List<Integer> arr) {

        long sum = 0;

        int size = arr.size();

        int candies [] = new int [size];

        candies[0] = 1;

        for(int i = 1; i < size; i++) {
            int candy = 1;
            if(arr.get(i) > arr.get(i-1)) {
                candy = candies[i-1]+1;
            }
            candies[i] = candy;
        }

        for(int j = size-1; j > 0; j--) {

            if(arr.get(j-1) > arr.get(j)) {
                candies[j-1] = Math.max(candies[j-1],candies[j]+1);
            }

            sum += candies[j];
        }

        sum += candies[0];

        return sum;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = Integer.parseInt(bufferedReader.readLine().trim());

        List<Integer> arr = IntStream.range(0, n).mapToObj(i -> {
            try {
                return bufferedReader.readLine().replaceAll("\\s+$", "");
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        })
                .map(String::trim)
                .map(Integer::parseInt)
                .collect(toList());

        long result = Result.candies(n, arr);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}

```

<br/>

### 파이썬 풀이

```python
#!/bin/python3

import math
import os
import random
import re
import sys

#
# Complete the 'candies' function below.
#
# The function is expected to return a LONG_INTEGER.
# The function accepts following parameters:
#  1. INTEGER n
#  2. INTEGER_ARRAY arr
#

def candies(n, arr):
    sum = 0;
    
    candies = [];
    candies.append(1);
    
    for i in range(1, len(arr), 1):
        candy = 1;
        if arr[i] > arr[i-1] :
            candy = candies[i-1]+1;
        candies.append(candy);
    
    for j in range(len(arr)-1, 0, -1):
        if arr[j-1] > arr[j]:
            candies[j-1] = max(candies[j-1],candies[j]+1);
        sum += candies[j];
        
    sum += candies[0];
    
    return sum;

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input().strip())

    arr = []

    for _ in range(n):
        arr_item = int(input().strip())
        arr.append(arr_item)

    result = candies(n, arr)

    fptr.write(str(result) + '\n')

    fptr.close()

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/maximum-perimeter-triangle/problem)