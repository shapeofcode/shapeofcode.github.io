---
layout: post
title:  "BOJ - 부분합"
date:   2022-01-27
last_modified_at: 2022-01-27
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 0.5초

메모리제한 128MB

<br/>

문제 유형 : 두 포인터

<br/>

문제 설명 간략 :    

10,000 이하의 자연수로 이루어진 길이 N짜리 수열이 주어진다.
이 수열에서 연속된 수들의 부분합 중에 그 합이 S 이상이 되는 것 중,
가장 짧은 것의 길이를 구하는 프로그램을 작성하시오.


<br/>

입력

첫째 줄에 N (10 ≤ N < 100,000)과 S (0 < S ≤ 100,000,000)가 주어진다.
둘째 줄에는 수열이 주어진다. 수열의 각 원소는 공백으로 구분되어져 있으며, 10,000이하의 자연수이다.



<br/>

출력

첫째 줄에 구하고자 하는 최소의 길이를 출력한다. 만일 그러한 합을 만드는 것이 불가능하다면 0을 출력하면 된다.




<br/>
   
접근법

두개의 포인터를 이용해 연속된 합이 S를 넘어서는 최소 길이를 구한다.


<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N;
    static int[][] info;

    static void input() {
        N = scan.nextInt();
        info = new int[N + 1][3];
        for (int i = 1; i <=N; i++) {
            for(int j = 0; j < 3; j++) info[i][j] = scan.nextInt();
        }
    }

    static int count(int A, int C, int B, int X) {
        if (X < A) return 0;
        if (C < X) return (C - A) / B + 1;
        return (X - A) / B + 1;
    }

    static boolean determination(int candidate) {
        long sum = 0;
        for(int i = 1; i <= N ; i++) {
            sum += count(info[i][0], info[i][1], info[i][2], candidate);
        }
        return sum % 2 == 1;
    }

    static void pro() {
        long L = 1, R = Integer.MAX_VALUE, ans = 0, ansCnt = 0;
        while(L <= R) {
            long mid = (L + R) / 2;
            if(determination((int) mid)) {
                ans = mid;
                R = mid - 1;
            } else {
                L = mid + 1;
            }
        }
        if (ans == 0) {
            System.out.println("NOTHING");
        } else {
            for (int i = 1; i <= N; i++) {
                if (info[i][0] <= ans && ans <= info[i][1] && (ans - info[i][0]) % info[i][2] == 0) {
                    ansCnt++;
                }
            }
            System.out.println(ans + " " + ansCnt);
        }
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

[BOJ 문제](https://www.acmicpc.net/problem/1806)