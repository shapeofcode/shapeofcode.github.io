---
layout: post
title:  "HackerRank - Largest Rectangle"
date:   2021-05-23
last_modified_at: 2021-05-23
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Stack and Queues

<br/>

문제 설명 간략 :    

높이가 다른 연속된 빌딩 중 가장 넓은 평평한 면적을 구하는 문제.

- 첫 번째 라인 n은 빌딩의 수이다.
- 두 번째 라인은 스페이스로 구분된 integers가 주어지고 빌딩의 높이이다.

<br/>

제약사항

- 1 <= n <= 10^5
- 1 <= h[i] <= 10^6

<br/>

idea 

1. 찾을 곳을 기준으로 앞뒤로 빌딩 높이를 계산하여 최대 면적을 구한다.
   

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
     * Complete the 'largestRectangle' function below.
     *
     * The function is expected to return a LONG_INTEGER.
     * The function accepts INTEGER_ARRAY h as parameter.
     */

    public static long largestRectangle(List<Integer> h) {

        long result = 0;
        int idx = 0;
        int size = h.size();

        while(idx < size) {

            int back = idx-1;
            int front = idx+1;



            while(back >= 0) {
                if(h.get(idx) > h.get(back)) {
                    back++;
                    break;
                }
                back--;
            }

            while(front < size) {
                if(h.get(idx) > h.get(front)) {
                    front--;
                    break;
                }
                front++;
            }

            if(back == -1) {
                back = 0;
            }
            if(front == size) {
                front = size-1;
            }

            long maxVal = h.get(idx)*((idx-back)+(front-idx)+1);

            if(result < maxVal) {
                result = maxVal;
            }

            idx++;
        }


        return result;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = Integer.parseInt(bufferedReader.readLine().trim());

        List<Integer> h = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                .map(Integer::parseInt)
                .collect(toList());

        long result = Result.largestRectangle(h);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/largest-rectangle/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=stacks-queues)