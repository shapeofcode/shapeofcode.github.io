---
layout: post
title:  "HackerRank - Max Min"
date:   2021-05-08
last_modified_at: 2021-05-08
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Greedy

<br/>

문제 설명 간략 : integer list와 k가 주어지고 k 크기의 arr를 주어진 list로 만든다.
k 크기의 arr에서 max(arr<sup>t</sup>)-min(arr<sup>t</sup>)의 최소값을 구하여라.

<br/>

제약사항

- 2 <= n <= 10^5
- 2 <= k <= n
- 0 <= arr[i] <= 10^9

<br/>

idea 

1. 정렬을 통해 그룹내의 최소값, 최대값을 쉽게 구할 수 있다.

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
     * Complete the 'maxMin' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER k
     *  2. INTEGER_ARRAY arr
     */

    public static int maxMin(int k, List<Integer> arr) {
        Collections.sort(arr);

        int result = Integer.MAX_VALUE;

        for(int i = 0; i < arr.size()-k+1; i++) {
            if(arr.get(i+k-1)-arr.get(i) < result) {
                result = arr.get(i+k-1)-arr.get(i);
            }
        }

        return result;

    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = Integer.parseInt(bufferedReader.readLine().trim());

        int k = Integer.parseInt(bufferedReader.readLine().trim());

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

        int result = Result.maxMin(k, arr);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/angry-children/problem)