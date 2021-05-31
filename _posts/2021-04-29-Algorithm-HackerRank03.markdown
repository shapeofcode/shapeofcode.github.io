---
layout: post
title:  "HackerRank - hackerland-radio-transmitters"
date:   2021-04-29
last_modified_at: 2021-04-29
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Greedy

<br/>

문제 설명 간략 : 직선 위에 집들이 위치해 있고 송신기가 모든 집을 커버 할 수 있게 설치해야한다. 송신기는 집에만 설치 될 수 있다.

<br/>

제약사항

- 1 <= n,k <= 10^5
- 1 <= x[i] <= 10^5

<br/>

idea 

1. 송신기는 앞뒤로 커버 가능하기 때문에 다음 집이 나오기 전까지 index를 늘려가며 커버 가능한 범위를 구한다. (먼저 정렬한다.)
2. 뒤도 동일
3. 마지막 집이 나올때까지 반복한다.

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
     * Complete the 'hackerlandRadioTransmitters' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER_ARRAY x
     *  2. INTEGER k
     */

    public static int hackerlandRadioTransmitters(List<Integer> x, int k) {

        Collections.sort(x);
        int transmitters = 0;
        int i = 0;
        int n = x.size();

        while(i < n) {
            transmitters++;
            int loc = x.get(i)+k;

            while (i < n && x.get(i) <= loc) {
                i++;
            }

            i--;
            loc = x.get(i) + k;

            while (i < n && x.get(i) <= loc) {
                i++;
            }

        }

        return transmitters;

    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int n = Integer.parseInt(firstMultipleInput[0]);

        int k = Integer.parseInt(firstMultipleInput[1]);

        List<Integer> x = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                .map(Integer::parseInt)
                .collect(toList());

        int result = Result.hackerlandRadioTransmitters(x, k);

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
# Complete the 'hackerlandRadioTransmitters' function below.
#
# The function is expected to return an INTEGER.
# The function accepts following parameters:
#  1. INTEGER_ARRAY x
#  2. INTEGER k
#

def hackerlandRadioTransmitters(x, k):
    x.sort()
    transmitters = 0
    i = 0
    n = len(x)
    
    while i < n:
        transmitters +=1
        loc = x[i]+k
        while i < n and x[i] <= loc:
            i +=1
        
        i -=1
        loc = x[i]+k
        
        while i < n and x[i] <= loc:
            i += 1
            
    return transmitters

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    first_multiple_input = input().rstrip().split()

    n = int(first_multiple_input[0])

    k = int(first_multiple_input[1])

    x = list(map(int, input().rstrip().split()))

    result = hackerlandRadioTransmitters(x, k)

    fptr.write(str(result) + '\n')

    fptr.close()

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/hackerland-radio-transmitters/problem)