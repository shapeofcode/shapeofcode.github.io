---
layout: post
title:  "HackerRank - Array Manipulation"
date:   2021-06-10
last_modified_at: 2021-06-10
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Hard

<br/>

문제 유형 : Data Structures - Arrays

<br/>

문제 설명 간략 :    

배열의 길이 n과 arrya가 담긴 list operation이 제공된다.
queries = [[1,5,3],[4,8,7],[6,9,1]]이 주어지고 배열 원소의 첫번째 두번쨰 원소는 n 위치의 시작점과 끝점을 의미하고
세번쨰 원소는 더할 값을 의미한다.

quries의 operation이 끝나고 n의 가장 큰 값을 구하여라.

<br/>

idea

그냥 돌면서 더하면 timeout이 발생한다. 누적합의 개념을 사용하면 연산의 속도를 높일 수 있다.

시작점에 세번째 원소 k를 더하고 끝점+1에 k를 뺀다 그렇게 되면 누적합을 구하였을 때 끝점+1 위치는 +k-k = 0이 되어 
앞부분만 k를 더한 값으로 계산이 된다.

<br/>

제약사항

- 3 <= n <= 10^7
- 1 <= m <= 2*10^5
- 1 <= a <= b <= n
- 0 <= k <= 10^9

<br/>
   

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
     * Complete the 'arrayManipulation' function below.
     *
     * The function is expected to return a LONG_INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER n
     *  2. 2D_INTEGER_ARRAY queries
     */

    public static long arrayManipulation(int n, List<List<Integer>> queries) {

        long [] array = new long[n];

        for(int i = 0; i < queries.size(); i++) {
            List<Integer> row = queries.get(i);
            int a = row.get(0);
            int b = row.get(1);
            int k = row.get(2);

            array[a-1] += k;
            if(b < n) {
                array[b] -= k;
            }

        }

        long maxValue = 0;
        long sum = 0;
        for(int i = 0; i < n; i++) {
            sum += array[i];
            maxValue = Math.max(maxValue, sum);
        }

        return maxValue;

    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int n = Integer.parseInt(firstMultipleInput[0]);

        int m = Integer.parseInt(firstMultipleInput[1]);

        List<List<Integer>> queries = new ArrayList<>();

        IntStream.range(0, m).forEach(i -> {
            try {
                queries.add(
                        Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                                .map(Integer::parseInt)
                                .collect(toList())
                );
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        });

        long result = Result.arrayManipulation(n, queries);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/crush/problem)