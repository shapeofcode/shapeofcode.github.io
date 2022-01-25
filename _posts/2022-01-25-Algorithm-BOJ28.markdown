---
layout: post
title:  "BOJ - 이상한 술집"
date:   2022-01-25
last_modified_at: 2022-01-25
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

프로그래밍 대회 전날, 은상과 친구들은 이상한 술집에 모였다.
이 술집에서 막걸리를 시키면 주전자의 용량은 똑같았으나 안에 들어 있는 막걸리 용량은 랜덤이다.  
즉 한 번 주문에 막걸리 용량이 802ml 이기도 1002ml가 나오기도 한다.  
은상은 막걸리 N 주전자를 주문하고, 자신을 포함한 친구들 K명에게 막걸리를 똑같은 양으로 나눠주려고 한다.
그런데 은상과 친구들은 다른 주전자의 막걸리가 섞이는 것이 싫어서,
분배 후 주전자에 막걸리가 조금 남아 있다면 그냥 막걸리를 버리기로 한다.  
(즉, 한 번 주문한 막걸리에 남은 것을 모아서 친구들에게 다시 주는 경우는 없다.  
예를 들어 5명이 3 주전자를 주문하여 1002, 802, 705 ml의 막걸리가 각 주전자에 담겨져 나왔고,
이것을 401ml로 동등하게 나눴을 경우 각각 주전자에서 200ml, 0m, 304ml 만큼은 버린다.)
이럴 때 K명에게 최대한의 많은 양의 막걸리를 분배할 수 있는 용량 ml는 무엇인지 출력해주세요.


<br/>

입력

첫째 줄에는 은상이가 주문한 막걸리 주전자의 개수 N,
그리고 은상이를 포함한 친구들의 수 K가 주어진다.
둘째 줄부터 N개의 줄에 차례로 주전자의 용량이 주어진다.
N은 10000이하의 정수이고, K는 1,000,000이하의 정수이다.
막걸리의 용량은 2^31 -1 보다 작거나 같은 자연수 또는 0이다.
단, 항상 N ≤ K 이다. 즉, 주전자의 개수가 사람 수보다 많을 수는 없다.


<br/>

출력

첫째 줄에 K명에게 나눠줄 수 있는 최대의 막걸리 용량 ml 를 출력한다.

<br/>
   
접근법

주전자 양을 막걸리 용량으로 나눴을때 수의 합이 줄 수 있는 친구들의 수 보다 많아 지는 조건의 최대 용량을 이분탐색으로 구한다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int K, N;
    static int[] A;

    static void input() {
        N = scan.nextInt();
        K = scan.nextInt();
        A = new int[N + 1];
        for(int i = 1; i <= N; i++) {
            A[i] = scan.nextInt();
        }
    }

    static boolean determination(long volume) {
        long sum = 0;
        for (int i = 1; i <= N; i++) {
            sum += A[i] / volume;
        }
        return sum >= K;

    }

    static void pro() {
        long L = 0, R = Integer.MAX_VALUE, ans = 0;

        while(L <= R) {
            long mid = (L + R) / 2;
            if(determination(mid)) {
                L = mid + 1;
                ans = mid;
            } else {
                R = mid - 1;
            }
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

[BOJ 문제](https://www.acmicpc.net/problem/13702)