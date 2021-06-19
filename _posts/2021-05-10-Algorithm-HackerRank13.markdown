---
layout: post
title:  "HackerRank - Max Array Sum"
date:   2021-05-10
last_modified_at: 2021-05-10
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Dynamic Programming

<br/>

문제 설명 간략 : integer 배열이 주어지고 인접하지 않은 원소들에 대한 부분집합의 합이 최대가 되는 값을 찾아라.

<br/>

제약사항

- 1 <= n <= 10^5
- 10^4 <= arr[i] <= 10^4

<br/>

idea 

1. 0번과 1번 원소 중 큰 값을 시작 값으로 정한다.
1. 현재 값이 최대가 되는 합의 값을 구한다 (현재 값과 인접하지 않은 다음 값의 합을 이전 값과 비교하여 큰 값을 구한다).

<br/>

### 자바 풀이

```java
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.regex.*;

public class Solution {

    // Complete the maxSubsetSum function below.
    static int maxSubsetSum(int[] arr) {

        int len = arr.length;

        if (len == 0) {
            return 0;
        }
        arr[0] = Math.max(0, arr[0]);
        if (len == 1) {
            return arr[0];
        }
        arr[1] = Math.max(arr[0], arr[1]);


        for(int i = 2; i < len; i++) {
            arr[i] = Math.max(arr[i-1], arr[i]+arr[i-2]);
        }

        return arr[len-1];

    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        int[] arr = new int[n];

        String[] arrItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < n; i++) {
            int arrItem = Integer.parseInt(arrItems[i]);
            arr[i] = arrItem;
        }

        int res = maxSubsetSum(arr);

        bufferedWriter.write(String.valueOf(res));
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/max-array-sum/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dynamic-programming)