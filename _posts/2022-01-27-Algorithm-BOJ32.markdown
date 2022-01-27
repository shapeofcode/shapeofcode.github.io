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

부분합을 구할 경우 투포인터를 이용하는데 연속된 합이 나오는 지점에서 멈추고 다음 오른쪽 포인터를 
한칸 움직인다. 생각해보면 다음 부분합은 멈춘 왼쪽 포인터보다는 더 가야한다.(오른쪽 포인터만큼의 양수를 제하였기떄문에)
다음 포인터를 이동하며 부분합이 S를 넘는 순간의 최소길이를 갱신한다.




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

    static int N, S;
    static int[] A;

    static void input() {
        N = scan.nextInt();
        S = scan.nextInt();
        A = new int[N+1];
        for(int i = 1; i <= N; i++) {
            A[i] = scan.nextInt();
        }
    }

    static void pro() {
        int R = 0, sum = 0, ans = N + 1;
        for(int L = 1; L <= N; L++) {
            sum -= A[L-1];
            while(R + 1 <=N && sum < S)
                sum += A[++R];

            if(sum >= S)
                ans = Math.min(ans, R - L + 1);
        }

        if(ans == N + 1)
            ans = 0;
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

[BOJ 문제](https://www.acmicpc.net/problem/1806)