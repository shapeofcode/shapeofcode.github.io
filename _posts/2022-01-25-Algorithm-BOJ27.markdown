---
layout: post
title:  "BOJ - 용돈 관리"
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

현우는 용돈을 효율적으로 활용하기 위해 계획을 짜기로 하였다. 
현우는 앞으로 N일 동안 자신이 사용할 금액을 계산하였고, 
돈을 펑펑 쓰지 않기 위해 정확히 M번만 통장에서 돈을 빼서 쓰기로 하였다. 
현우는 통장에서 K원을 인출하며, 통장에서 뺀 돈으로 하루를 보낼 수 있으면 그대로 사용하고, 
모자라게 되면 남은 금액은 통장에 집어넣고 다시 K원을 인출한다. 
다만 현우는 M이라는 숫자를 좋아하기 때문에, 
정확히 M번을 맞추기 위해서 남은 금액이 그날 사용할 금액보다 많더라도 남은 금액은 통장에 집어넣고 다시 K원을 인출할 수 있다. 
현우는 돈을 아끼기 위해 인출 금액 K를 최소화하기로 하였다. 현우가 필요한 최소 금액 K를 계산하는 프로그램을 작성하시오.

<br/>

입력

1번째 줄에는 N과 M이 공백으로 주어진다. (1 ≤ N ≤ 100,000, 1 ≤ M ≤ N)

2번째 줄부터 총 N개의 줄에는 현우가 i번째 날에 이용할 금액이 주어진다. (1 ≤ 금액 ≤ 10000)

<br/>

출력

첫 번째 줄에 현우가 통장에서 인출해야 할 최소 금액 K를 출력한다.

<br/>
   
접근법

인출한 돈보다 사용 금액이 큰 경우 카운트를 늘려주고 재인출을 하며 이분 탐색으로 인출할 최소 금액을 구한다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {

    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N, M;
    static int[] A;

    static void input() {
        N = scan.nextInt();
        M = scan.nextInt();
        A = new int[N + 1];
        for(int i = 1;i <= N; i++) {
            A[i] = scan.nextInt();
        }
    }

    static boolean determination(int withdrawl) {
        int cnt = 1, sum = 0;

        for(int i = 1; i <= N; i++) {
            if(sum+A[i] > withdrawl) {
                cnt++;
                sum = A[i];
            } else {
                sum += A[i];
            }
        }

        return cnt <= M;
    }

    static void pro() {
        int L = A[1], R = 100000, ans = 0;
        for(int i = 1; i <= N; i++) L = Math.max(L, A[i]);

        while(L <= R) {
            int mid = (L + R) / 2;
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

[BOJ 문제](https://www.acmicpc.net/problem/6236)