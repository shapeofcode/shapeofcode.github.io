---
layout: post
title:  "BOJ - K번째 수"
date:   2022-01-27
last_modified_at: 2022-01-27
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 128MB

<br/>

문제 유형 : 이분탐색

<br/>

문제 설명 간략 :    

세준이는 크기가 N×N인 배열 A를 만들었다.
배열에 들어있는 수 A[i][j] = i×j 이다.
이 수를 일차원 배열 B에 넣으면 B의 크기는 N×N이 된다.
B를 오름차순 정렬했을 때, B[k]를 구해보자.

배열 A와 B의 인덱스는 1부터 시작한다.




<br/>

입력

첫째 줄에 배열의 크기 N이 주어진다.
N은 10^5보다 작거나 같은 자연수이다.
둘째 줄에 k가 주어진다. k는 min(10^9, N^2)보다 작거나 같은 자연수이다.



<br/>

출력

B[k]를 출력한다.


<br/>
   
접근법

B[k]보다 작은 수가 B[k] 보다 작으면 안되는 조건을 이분탐색으로 찾는다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N, K;

    static void input() {
        N = scan.nextInt();
        K = scan.nextInt();
    }

    static boolean determination(long candidate) {
        long sum = 0;
        for(int i = 1; i <=N; i++) {
            sum += Math.min(N, candidate / i);
        }
        return sum >= K;
    }

    static void pro() {
        long L = 1, R = (long) N * N, ans = 0;
        while(L <= R) {
            long mid = (L + R) / 2;
            if(determination(mid)) {
                ans = mid;
                R = mid - 1;
            } else {
                L = mid + 1;
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

[BOJ 문제](https://www.acmicpc.net/problem/1300)