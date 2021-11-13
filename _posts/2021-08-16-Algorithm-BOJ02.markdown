---
layout: post
title:  "BOJ - N과 M(1)"
date:   2021-08-16
last_modified_at: 2021-08-16
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 1초

메모리제한 512MB

<br/>

문제 유형 : 완전탐색

<br/>

문제 설명 간략 :    

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

- 1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열


<br/>

입력

첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)

<br/>

출력

한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.

수열은 사전 순으로 증가하는 순서로 출력해야 한다.

<br/>
   
접근법

사용되었는지 체크를 하는 반복문 사용, 재귀호출로 값 할당.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();
    
    static void input() {
        N = scan.nextInt();
        M = scan.nextInt();
        selected = new int[M + 1];
    }
    
    static int N, M;
    static int[] selected;
    
    static void rec_func(int k) {
        if (k == M + 1) {
            for(int i = 1; i <= M; i++) sb.append(selected[i]).append(' ');
            sb.append('\n');
        } else {
            for (int cand = 1; cand <= N; cand++) {
                boolean isUsed = false;
                for(int i=1; i < k ; i++) {
                    if(cand == selected[i]) {
                        isUsed = true;
                    }
                }
                if(!isUsed) {
                    selected[k] = cand;
                    rec_func(k + 1);
                    selected[k] = 0;
                }
            }
        }
    }
    
    public static void main(String[] args) {
        input();
        rec_func(1);
        System.out.println(sb.toString());
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

[BOJ 문제](https://www.acmicpc.net/problem/15649)