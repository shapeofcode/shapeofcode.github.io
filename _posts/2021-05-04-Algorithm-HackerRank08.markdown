---
layout: post
title:  "HackerRank - Pairs"
date:   2021-05-04
last_modified_at: 2021-05-04
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Search

<br/>

문제 설명 간략 : 배열과 타겟 값이 주어진다. 배열의 두 값의 차이가 타겟값과 같아 지는 쌍의 갯수를 찾아라.


<br/>

제약사항

- 2 <= k <= 10^5
- 0 < k < 10^9
- 0 <= arr[i] <= 2^31-1
- arr[i]의 integer는 unique하다

<br/>

idea 

1. hashset에 값들을 담는다.
2. loop를 돌면서 값+k에 해당하는 원소가 있는지 찾는다.

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
     * Complete the 'pairs' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER k
     *  2. INTEGER_ARRAY arr
     */

    public static int pairs(int k, List<Integer> arr) {

        HashSet<Integer> set = new HashSet<Integer>();

        int pairs = 0;

        for(int i = 0;  i < arr.size(); i++) {
            set.add(arr.get(i));
        }

        for(int j = 0;  j < arr.size(); j++) {
            if(set.contains(arr.get(j) + k)) {
                pairs++;
            }
        }

        return pairs;

    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int n = Integer.parseInt(firstMultipleInput[0]);

        int k = Integer.parseInt(firstMultipleInput[1]);

        List<Integer> arr = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                .map(Integer::parseInt)
                .collect(toList());

        int result = Result.pairs(k, arr);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/pairs/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=search)