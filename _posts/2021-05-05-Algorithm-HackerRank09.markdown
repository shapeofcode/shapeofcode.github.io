---
layout: post
title:  "HackerRank - Triple sum"
date:   2021-05-05
last_modified_at: 2021-05-05
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Search

<br/>

문제 설명 간략 : 세 개의 배열이 주어지고 p,q,r은 각 배열에 속하는 원소이며 p <= q && q >= r을 만족하는 세개의 쌍을 구하라.


<br/>

제약사항

- 1 <= lena,lenb,lenc <= 10^5
- 1 <= all elements in a,b,c <= 10^8

<br/>

idea 

1. 각 배열의 인덱스를 사용해 중간 원소를 기준으로 앞 배열과 뒷 배열의 조합을 구한다. (배열의 중복 값을 제거한다.)

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

    // Complete the triplets function below.
    static long triplets(int[] a, int[] b, int[] c) {

        int[] _a = Arrays.stream(a).sorted().distinct().toArray();
        int[] _b = Arrays.stream(b).sorted().distinct().toArray();
        int[] _c = Arrays.stream(c).sorted().distinct().toArray();

        int i = 0;
        int j = 0;
        int k = 0;
        long total = 0;

        while(j < _b.length) {
            while(i < _a.length && _a[i] <= _b[j])
                i++;

            while(k < _c.length && _c[k] <= _b[j])
                k++;

            total += (long)i * k;
            j++;
        }

        return total;

    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] lenaLenbLenc = scanner.nextLine().split(" ");

        int lena = Integer.parseInt(lenaLenbLenc[0]);

        int lenb = Integer.parseInt(lenaLenbLenc[1]);

        int lenc = Integer.parseInt(lenaLenbLenc[2]);

        int[] arra = new int[lena];

        String[] arraItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < lena; i++) {
            int arraItem = Integer.parseInt(arraItems[i]);
            arra[i] = arraItem;
        }

        int[] arrb = new int[lenb];

        String[] arrbItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < lenb; i++) {
            int arrbItem = Integer.parseInt(arrbItems[i]);
            arrb[i] = arrbItem;
        }

        int[] arrc = new int[lenc];

        String[] arrcItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < lenc; i++) {
            int arrcItem = Integer.parseInt(arrcItems[i]);
            arrc[i] = arrcItem;
        }

        long ans = triplets(arra, arrb, arrc);

        bufferedWriter.write(String.valueOf(ans));
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/triple-sum/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=search)