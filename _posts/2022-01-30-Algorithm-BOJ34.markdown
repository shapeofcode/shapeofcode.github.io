---
layout: post
title:  "BOJ - List of Unique Numbers"
date:   2022-01-30
last_modified_at: 2022-01-30
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 1초

메모리제한 32MB

<br/>

문제 유형 : 두 포인터

<br/>

문제 설명 간략 :    

길이가 N인 수열이 주어질 때, 수열에서 연속한 1개 이상의 수를 뽑았을 때 
같은 수가 여러 번 등장하지 않는 경우의 수를 구하는 프로그램을 작성하여라.

<br/>

입력

첫 번째 줄에는 수열의 길이 N이 주어진다. (1 ≤ N ≤ 100,000)

두 번째 줄에는 수열을 나타내는 N개의 정수가 주어진다. 수열에 나타나는 수는 모두 1 이상 100,000 이하이다.

<br/>

출력

조건을 만족하는 경우의 수를 출력한다.

<br/>
   
접근법

투 포인터를 이용해서 R 값은 동일한 수가 나오기 전까지 계속 옮겨주고 정답에 카운트를 갱신한다.

그다음 경우의 수는 L 값을 옮기고 다음 R 값부터 카운트를 하는데 기존의 L값은 제외하고 움직인다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N;
    static int[] A, cnt;

    static void input() {
        N = scan.nextInt();
        A = new int[N+1];
        for(int i = 1; i <= N; i++) {
            A[i] = scan.nextInt();
        }
        cnt = new int[100000 + 1];
    }

    static void pro() {
        long ans = 0;
        
        for (int L=1, R=0; L<=N; L++) {
            while(R + 1 <= N && cnt[A[R+1]] == 0) {
                R++;
                cnt[A[R]]++;
            }
            
            ans += R - L + 1;
            cnt[A[L]]--;
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

[BOJ 문제](https://www.acmicpc.net/problem/13144)