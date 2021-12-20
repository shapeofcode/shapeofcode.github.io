---
layout: post
title:  "BOJ - 카드"
date:   2021-08-27
last_modified_at: 2021-08-27
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 1초

메모리제한 256MB

<br/>

문제 유형 : 정렬

<br/>

문제 설명 간략 :    

준규는 숫자 카드 N장을 가지고 있다. 숫자 카드에는 정수가 하나 적혀있는데, 적혀있는 수는 -262보다 크거나 같고, 262보다 작거나 같다.

준규가 가지고 있는 카드가 주어졌을 때, 가장 많이 가지고 있는 정수를 구하는 프로그램을 작성하시오. 만약, 가장 많이 가지고 있는 정수가 
여러 가지라면, 작은 것을 출력한다.

<br/>

입력

첫째 줄에 준규가 가지고 있는 숫자 카드의 개수 N (1 ≤ N ≤ 100,000)이 주어진다. 
둘째 줄부터 N개 줄에는 숫자 카드에 적혀있는 정수가 주어진다.

<br/>

출력

첫째 줄에 준규가 가장 많이 가지고 있는 정수를 출력한다.
 
<br/>
   
접근법

정렬 후 최빈값, 최빈값의 등장 횟수, 현재 값의 등장 회수를 구한다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();
    
    static int N;
    static long[] a;
    
    static void input() {
        N = scan.nextInt();
        a = new long[N+1];
        for (int i = 1; i < N; i++) {
            B[i] = scan.nextLong();
        }
    }
    
    static void pro() {
        Arrays.sort(a, 1, N + 1);
        long mode = a[1];
        int modeCnt = 1, curCnt = 1;
        
        for (int i = 2; i <= N; i++) {
            if (a[i] == a[i - 1]) {
                curCnt++;
            } else {
                curCnt = 1;
            }
            
            if (curCnt > modeCnt) {
                modeCnt = curCnt;
                mode = a[i];
            }
        }
        System.out.println(mode);
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

[BOJ 문제](https://www.acmicpc.net/problem/11652)