---
layout: post
title:  "BOJ - 공유기 설치"
date:   2022-01-06
last_modified_at: 2022-01-06
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 1초

메모리제한 256MB

<br/>

문제 유형 : 이분탐색

<br/>

문제 설명 간략 :    

도현이의 집 N개가 수직선 위에 있다. 각각의 집의 좌표는 x1, ..., xN이고, 집 여러개가 같은 좌표를 가지는 일은 없다.

도현이는 언제 어디서나 와이파이를 즐기기 위해서 집에 공유기 C개를 설치하려고 한다. 
최대한 많은 곳에서 와이파이를 사용하려고 하기 때문에, 한 집에는 공유기를 하나만 설치할 수 있고, 
가장 인접한 두 공유기 사이의 거리를 가능한 크게 하여 설치하려고 한다.

C개의 공유기를 N개의 집에 적당히 설치해서, 가장 인접한 두 공유기 사이의 거리를 최대로 하는 프로그램을 작성하시오.

<br/>

입력

첫째 줄에 집의 개수 N (2 ≤ N ≤ 200,000)과 공유기의 개수 C (2 ≤ C ≤ N)이 하나 이상의 빈 칸을 사이에 두고 주어진다. 
둘째 줄부터 N개의 줄에는 집의 좌표를 나타내는 xi (0 ≤ xi ≤ 1,000,000,000)가 한 줄에 하나씩 주어진다.

<br/>

출력

첫째 줄에 가장 인접한 두 공유기 사이의 최대 거리를 출력한다.
 
<br/>
   
접근법

거리를 던져주고 이분 탐색으로 가능한 와이파이 갯수 조건에 만족하는지 확인한 후 최대 거리를 좁혀 나간다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {

    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N, C;
    static int[] A;

    static void input() {
        N = scan.nextInt();
        C = scan.nextInt();
        A = new int[N + 1];
        for (int i = 1; i <= N; i++) {
            A[i] = scan.nextInt();
        }
    }

    static boolean determination(int D) {
        int cnt = 1, last = A[1];
        for(int i = 2; i <= N; i++) {
            if(A[i] - last < D) continue;
            last = A[i];
            cnt++;
        }
        return cnt >= C;
    }

    static void pro() {
        Arrays.sort(A, 1, N + 1);

        int L = 1, R = 1000000000, ans = 0;

        while (L <= R) {
            int mid = (L + R) / 2;
            if (determination(mid)) {
                ans = mid;
                L = mid + 1;
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

[BOJ 문제](https://www.acmicpc.net/problem/2110)