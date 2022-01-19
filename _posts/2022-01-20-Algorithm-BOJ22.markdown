---
layout: post
title:  "BOJ - 두 수의 합"
date:   2022-01-20
last_modified_at: 2022-01-20
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 1초

메모리제한 128MB

<br/>

문제 유형 : 이분탐색

<br/>

문제 설명 간략 :    

n개의 서로 다른 양의 정수 a1, a2, ..., an으로 이루어진 수열이 있다. ai의 값은 1보다 크거나 같고, 
1000000보다 작거나 같은 자연수이다. 
자연수 x가 주어졌을 때, ai + aj = x (1 ≤ i < j ≤ n)을 만족하는 (ai, aj)쌍의 수를 구하는 프로그램을 작성하시오.

<br/>

입력

첫째 줄에 수열의 크기 n이 주어진다. 다음 줄에는 수열에 포함되는 수가 주어진다. 셋째 줄에는 x가 주어진다. 
(1 ≤ n ≤ 100000, 1 ≤ x ≤ 2000000)

<br/>

출력

문제의 조건을 만족하는 쌍의 개수를 출력한다.
 
<br/>
   
접근법

주어진 input 배열을 정렬하고 순서대로 비교할 대상(합에서 뺀 나머지를 이분 탐색으로 찾는다.)

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {

    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N, Sum;
    static int[] A;

    static void input() {
        N = scan.nextInt();
        A = new int[N + 1];
        for(int i = 1; i <= N; i++) {
            A[i] = scan.nextInt();
        }
        Sum = scan.nextInt();
    }

    static boolean bin_search(int[] A, int L, int R, int X) {

        while(L <= R) {
            int mid = (L+R) / 2;
            if(A[mid] == X)
                return true;

            if(A[mid] < X)
                L = mid + 1;
            else
                R = mid - 1;
        }
        return false;

    }

    static void pro() {
        Arrays.sort(A, 1, N + 1);
        int ans = 0;
        for(int i = 1; i <= N - 1; i++) {
            if(bin_search(A, i + 1, N, Sum-A[i])) ans++;
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

[BOJ 문제](https://www.acmicpc.net/problem/3273)