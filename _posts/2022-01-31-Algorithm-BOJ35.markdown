---
layout: post
title:  "BOJ - 좋다"
date:   2022-01-31
last_modified_at: 2022-01-31
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 256MB

<br/>

문제 유형 : 두 포인터

<br/>

문제 설명 간략 :    

N개의 수 중에서 어떤 수가 다른 수 두 개의 합으로 나타낼 수 있다면 그 수를 “좋다(GOOD)”고 한다.

N개의 수가 주어지면 그 중에서 좋은 수의 개수는 몇 개인지 출력하라.

수의 위치가 다르면 값이 같아도 다른 수이다.

<br/>

입력

첫째 줄에는 수의 개수 N(1 ≤ N ≤ 2,000), 두 번째 줄에는 i번째 수를 나타내는 Ai가 N개 주어진다. 
(|Ai| ≤ 1,000,000,000, Ai는 정수)

<br/>

출력

좋은 수의 개수를 첫 번째 줄에 출력한다.

<br/>
   
접근법

최소, 최대를 빠르게 알기 위해 정렬하고 투 포인터를 이용해 양 끝 지점의 합이 타겟보타 클 경우 오른쪽 감소,
같을 경우는 true 그 외에는 왼쪽을 증가 시키며 왼쪽이 오른쪽보다 커질 때까지 합으로 표현된 값이 없을 경우 false를 반환한다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N;
    static int[] A;

    static void input() {
        N = scan.nextInt();
        A = new int[N+1];
        for(int i = 1; i <= N; i++) {
            A[i] = scan.nextInt();
        }
    }

    static boolean func(int idx) {
        int L = 1, R = N;
        int target = A[idx];
        while(L < R) {
            if(L == idx) L++;
            else if(R == idx) R--;
            else {
                if (A[L] + A[R] > target) R--;
                else if (A[L] + A[R] == target) return true;
                else L++;
            }
        }
        return false;
    }
    
    static void pro() {
        Arrays.sort(A, 1, N + 1);
        
        int ans = 0;
        for (int i = 1; i <= N; i++) {
            if (func(i)) ans++;
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

[BOJ 문제](https://www.acmicpc.net/problem/1253)