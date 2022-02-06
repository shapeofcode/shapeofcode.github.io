---
layout: post
title:  "BOJ - 수들의 합 2"
date:   2022-02-06
last_modified_at: 2022-02-06
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 0.5초

메모리제한 128MB

<br/>

문제 유형 : 두 포인터

<br/>

문제 설명 간략 :    

N개의 수로 된 수열 A[1], A[2], …, A[N] 이 있다. 
이 수열의 i번째 수부터 j번째 수까지의 합 A[i] + A[i+1] + … + A[j-1] + A[j]가 M이 되는 경우의 수를 구하는 프로그램을 작성하시오.

<br/>

입력

첫째 줄에 N(1 ≤ N ≤ 10,000), M(1 ≤ M ≤ 300,000,000)이 주어진다. 
다음 줄에는 A[1], A[2], …, A[N]이 공백으로 분리되어 주어진다. 각각의 A[x]는 30,000을 넘지 않는 자연수이다.

<br/>

출력

첫째 줄에 경우의 수를 출력한다.

<br/>
   
접근법

두 포인터를 사용하여 L은 움직이면서 기존껀 제외하고 
R을 n보다는 작으면서 합보다는 작을때까지 이동시키며 조건에 맞으면 카운트를 늘려준다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static StringBuilder sb = new StringBuilder();
    static FastReader scan = new FastReader();

    static int n, S;
    static int[] a;

    static void input() {
        n = scan.nextInt();
        S = scan.nextInt();
        a = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            a[i] = scan.nextInt();
        }
    }

    static void pro() {
        int R = 0, sum = 0, ans = 0;
        for (int L = 1; L <= n; L++) {
            // L - 1 을 구간에서 제외하기
            sum -= a[L - 1];

            // R 을 옮길 수 있을 때 까지 옮기기
            while (R + 1 <= n && sum < S)
                sum += a[++R];

            // [L ... R] 의 합, 즉 sum이 조건을 만족하면 정답 갱신하기
            if (sum == S)
                ans++;
        }

        System.out.println(ans);
    }

    public static void main(String[] args) {
        input();
        pro();
    }

    static class FastReader {
        BufferedReader br;
        StringTokenizer st;

        public FastReader() {
            br = new BufferedReader(new InputStreamReader(System.in));
        }

        public FastReader(String s) throws FileNotFoundException {
            br = new BufferedReader(new FileReader(new File(s)));
        }

        String next() {
            while (st == null || !st.hasMoreElements()) {
                try {
                    st = new StringTokenizer(br.readLine());
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            return st.nextToken();
        }

        int nextInt() {
            return Integer.parseInt(next());
        }

        long nextLong() {
            return Long.parseLong(next());
        }

        double nextDouble() {
            return Double.parseDouble(next());
        }

        String nextLine() {
            String str = "";
            try {
                str = br.readLine();
            } catch (IOException e) {
                e.printStackTrace();
            }
            return str;
        }
    }
}

```

<br/>

출처

[BOJ 문제](https://www.acmicpc.net/problem/2003)