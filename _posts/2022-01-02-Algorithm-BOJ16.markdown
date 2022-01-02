---
layout: post
title:  "BOJ - 먹을 것인가 먹힐 것인가"
date:   2022-01-02
last_modified_at: 2022-01-02
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

심해에는 두 종류의 생명체 A와 B가 존재한다. A는 B를 먹는다. A는 자기보다 크기가 작은 먹이만 먹을 수 있다. 
예를 들어, A의 크기가 {8, 1, 7, 3, 1}이고, B의 크기가 {3, 6, 1}인 경우에 A가 B를 먹을 수 있는 쌍의 개수는 7가지가 있다. 
8-3, 8-6, 8-1, 7-3, 7-6, 7-1, 3-1.
두 생명체 A와 B의 크기가 주어졌을 때, A의 크기가 B보다 큰 쌍이 몇 개나 있는지 구하는 프로그램을 작성하시오.

<br/>

입력

첫째 줄에 테스트 케이스의 개수 T가 주어진다. 각 테스트 케이스의 첫째 줄에는 A의 수 N과 B의 수 M이 주어진다. 
둘째 줄에는 A의 크기가 모두 주어지며, 셋째 줄에는 B의 크기가 모두 주어진다. 크기는 양의 정수이다. (1 ≤ N, M ≤ 20,000)

<br/>

출력

각 테스트 케이스마다, A가 B보다 큰 쌍의 개수를 출력한다.
 
<br/>
   
접근법

찾으려고 하는 집합을 정렬 후 이분 탐색

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N, M;
    static int[] A, B;

    static void input() {
        N = scan.nextInt();
        M = scan.nextInt();
        A = new int[N + 1];
        B = new int[M + 1];
        for (int i = 1; i <= N; i++) {
            A[i] = scan.nextInt();
        }
        for (int i = 1; i <= M; i++) {
            B[i] = scan.nextInt();
        }
    }

    static int lower_bound(int[] A, int L, int R, int X) {
        // A[L...R] 에서 X 미만의 수 중 제일 오른쪽 인덱스를 return 하는 함수
        // 그런 게 없다면 L - 1 을 return 한다

        int res = L - 1;  // 만약 A[L...R] 중 X 이하의 수가 없다면 L - 1 을 return 한다.
        while (L <= R) {
            int mid = (L + R) / 2;
            if (A[mid] < X) {
                res = mid;
                L = mid + 1;
            } else {
                R = mid - 1;
            }
        }
        return res;
    }

    static void pro() {
        // B 배열에 대해 이분탐색을 할 예정이니까, 정렬을 해주자!
        Arrays.sort(B, 1, M + 1);

        int ans = 0;
        for (int i = 1; i <= N; i++) {
            // A[i] 를 선택했을 때, B 에서는 A[i]보다 작은 게 몇 개나 있는 지 count하기
            ans += lower_bound(B, 1, M, A[i]);
        }
        System.out.println(ans);
    }

    public static void main(String[] args) {
        int TT;
        TT = scan.nextInt();
        for (int tt = 1; tt <= TT; tt++) {
            input();
            pro();
        }
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

[BOJ 문제](https://www.acmicpc.net/problem/7795)