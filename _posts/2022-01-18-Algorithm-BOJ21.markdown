---
layout: post
title:  "BOJ - 듣보잡"
date:   2022-01-18
last_modified_at: 2022-01-18
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 256MB

<br/>

문제 유형 : 이분탐색

<br/>

문제 설명 간략 :    

김진영이 듣도 못한 사람의 명단과, 보도 못한 사람의 명단이 주어질 때, 듣도 보도 못한 사람의 명단을 구하는 프로그램을 작성하시오.

<br/>

입력

첫째 줄에 듣도 못한 사람의 수 N, 보도 못한 사람의 수 M이 주어진다. 
이어서 둘째 줄부터 N개의 줄에 걸쳐 듣도 못한 사람의 이름과, N+2째 줄부터 보도 못한 사람의 이름이 순서대로 주어진다. 
이름은 띄어쓰기 없이 알파벳 소문자로만 이루어지며, 그 길이는 20 이하이다. N, M은 500,000 이하의 자연수이다.

듣도 못한 사람의 명단에는 중복되는 이름이 없으며, 보도 못한 사람의 명단도 마찬가지이다.

<br/>

출력

듣보잡의 수와 그 명단을 사전순으로 출력한다.
 
<br/>
   
접근법

비교할 배열을 정렬하고 원소를 이분탐색해서 찾는다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {

    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N;
    static String[] A, ans;

    static void input() {
        N = scan.nextInt();
        A = new String[N + 1];
        for (int i = 1; i <= N; i++) {
            A[i] = scan.nextLine();
        }
    }

    static boolean bin_search(int[] A, int L,int R, int X) {
        while (L <= R){
            int mid = (L+R)/2;
            if(A[mid].equals(X))
                return true;

            if(A[mid].compareTo(X) < 0)
                L = mid + 1;
            else
                R = mid - 1;
        }
        return false;
    }

    static void pro() {
        int M = scan.nextInt(), ansCnt = 0;
        ans = new String[N + 1];
        Arrays.sort(A, 1, N + 1);
        for(int i = 1; i <= M; i++) {
            String X = scan.nextLine();
            if (bin_search(A, 1, N, X)) ans[++ansCnt] = X;
        }
        Arrays.sort(ans, 1, ansCnt + 1);
        sb.append(ansCnt).append('\n');
        for (int i = 1; i <= ansCnt; i++) sb.append(ans[i]).append('\n');
        System.out.println(sb);
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

[BOJ 문제](https://www.acmicpc.net/problem/1764)