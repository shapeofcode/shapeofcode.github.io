---
layout: post
title:  "HackerRank - Maximum Perimeter Triangle"
date:   2021-04-25
last_modified_at: 2021-04-25
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Greedy

<br/>

문제 설명 간략 : 스틱 길이로 주어진 배열을 가지고 정상적인 최대 길이의 삼각형을 만들어라. 

- maximum 값이 여러개일 경우 가장 긴 녀석을 골라라.
- 정상적인 삼각형이 없으면 -1을 출력하라.

<br/>

제약사항

- 3 <= n <= 50
- 1 <= sticks[i] <= 10^9

<br/>

idea 

1. 삼각형 두 변의 합은 나머지 한변의 길이보다 길어야 한다.
2. sorting된 녀석들을 뒤에서 부터 탐색하면 최대 값을 좀 더 빨리 구할 수 있다.

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
     * Complete the 'maximumPerimeterTriangle' function below.
     *
     * The function is expected to return an INTEGER_ARRAY.
     * The function accepts INTEGER_ARRAY sticks as parameter.
     */

    public static List<Integer> maximumPerimeterTriangle(List<Integer> sticks) {
    // Write your code here
    
        Collections.sort(sticks);
        
        List<Integer> longestPerimeter = new ArrayList<Integer>();
        
        for(int i = sticks.size()-1; i > 1; i--) {
            if((sticks.get(i) < sticks.get(i-1)+sticks.get(i-2)) ||
                ((sticks.get(i) == sticks.get(i-1)) && (sticks.get(i) == sticks.get(i-2)))) {
                longestPerimeter.add(sticks.get(i-2));
                longestPerimeter.add(sticks.get(i-1));
                longestPerimeter.add(sticks.get(i));
                break;
            }
        }
        
        if(longestPerimeter.size() == 0) {
            longestPerimeter.add(-1);
        }
        
        return longestPerimeter;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = Integer.parseInt(bufferedReader.readLine().trim());

        List<Integer> sticks = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Integer::parseInt)
            .collect(toList());

        List<Integer> result = Result.maximumPerimeterTriangle(sticks);

        bufferedWriter.write(
            result.stream()
                .map(Object::toString)
                .collect(joining(" "))
            + "\n"
        );

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
# Complete the 'maximumPerimeterTriangle' function below.
#
# The function is expected to return an INTEGER_ARRAY.
# The function accepts INTEGER_ARRAY sticks as parameter.
#

def maximumPerimeterTriangle(sticks):
    sticks.sort()
    
    maximumTriangle = []
    
    for i in range(len(sticks)-1, 1, -1):
        if (sticks[i] < sticks[i-1]+sticks[i-2]) or ((sticks[i] == sticks[i-1]) and (sticks[i] == sticks[i-2])):
            maximumTriangle = [sticks[i-2], sticks[i-1], sticks[i]]
            break;
    
    
    if len(maximumTriangle) == 0:
        maximumTriangle = [-1]
        
    return maximumTriangle
            
        

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input().strip())

    sticks = list(map(int, input().rstrip().split()))

    result = maximumPerimeterTriangle(sticks)

    fptr.write(' '.join(map(str, result)))
    fptr.write('\n')

    fptr.close()

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/maximum-perimeter-triangle/problem)