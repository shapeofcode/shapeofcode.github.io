---
layout: post
title:  "BOJ - 부분수열의 합"
date:   2021-08-21
last_modified_at: 2021-08-21
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 256MB

<br/>

문제 유형 : 완전탐색

<br/>

문제 설명 간략 :    

N개의 정수로 이루어진 수열이 있을 때, 크기가 양수인 부분수열 중에서 그 수열의 원소를 다 더한 값이 S가 되는 경우의 수를 구하는 프로그램을 작성하시오.


<br/>

입력

첫째 줄에 정수의 개수를 나타내는 N과 정수 S가 주어진다. (1 ≤ N ≤ 20, |S| ≤ 1,000,000) 둘째 줄에 N개의 정수가 빈 칸을 사이에 두고 주어진다. 주어지는 정수의 절댓값은 100,000을 넘지 않는다.

<br/>

출력

첫째 줄에 합이 S가 되는 부분수열의 개수를 출력한다.

<br/>
   
접근법

k번째 원소를 포함시킬 지 안 포함시킬지 결정하고 재귀호출.

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
        S = scan.nextInt();
        nums = new int[N + 1];
        for (int i = 1; i <= N; i++) nums[i] = scan.nextInt();
    }
    
    static int N, S, ans;
    static int[] nums;
    
    static void rec_func(int k, int value) {
        if(k == N + 1) {
            if (value == S) ans ++;
        } else {
            rec_func(k + 1, value + nums[k]);
            rec_func(k + 1, value);
        }
    }
    
    public static void main(String[] args) {
        input();
        rec_func(1, 0);
        
        if (S == 0) {
            ans--;
        }
        System.out.println(ans);
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

[BOJ 문제](https://www.acmicpc.net/problem/1182)