---
layout: post
title:  "HackerRank - Count Triplets"
date:   2021-05-01
last_modified_at: 2021-05-01
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Dictionaries and HashMaps

<br/>

문제 설명 간략 : 정렬과 중복되지 않은 1부터 n까지의 배열이 제공되고 최소 swap을 하여 오름차순으로 정렬하라.


<br/>

제약사항

- 1 <= n <= 10^5
- 1 <= arr[i] <= n

<br/>

idea 

1. 배열을 돌면서 인덱스+1 값을 찾고 swap 해준다.

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

    // Complete the minimumSwaps function below.
    static int minimumSwaps(int[] arr) {

        int swap=0;

        for(int i=0; i<arr.length; i++){
            if(i+1 != arr[i]){
                int t=i;
                while(arr[t] != i+1){
                    t++;
                }
                arr[t]=arr[i];
                arr[i]=i+1;
                swap++;
            }
        }
        return swap;
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

        int res = minimumSwaps(arr);

        bufferedWriter.write(String.valueOf(res));
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/minimum-swaps-2/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays)