---
layout: post
title:  "BOJ - 화살표 그리기"
date:   2021-08-29
last_modified_at: 2021-08-29
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 512MB

<br/>

문제 유형 : 정렬

<br/>

문제 설명 간략 :    

직선 위에 위치를 나타내는 0, 1, 2, ...와 같은 음수가 아닌 정수들이 일정한 간격으로 오른쪽 방향으로 놓여 있다. 이러한 위치들 중 N개의 위치에 하나씩 점들이 주어진다.
각 점 p에 대해서, p에서 시작하는 직선 화살표를 이용해서 다른 점 q에 연결하려고 한다. 여기서, 점 q는 p와 같은 색깔의 점들 중 p와 거리가 가장 가까운 점이어야 한다. 만약 가장 가까운 점이 두 개 이상이면 아무거나 하나를 선택한다.
모든 점에 대해서 같은 색깔을 가진 다른 점이 항상 존재한다. 따라서 각 점 p에서 시작하여 위 조건을 만족하는 q로 가는 하나의 화살표를 항상 그릴 수 있다.
점들의 위치와 색깔이 주어질 때, 모든 점에서 시작하는 화살표들의 길이 합을 출력하는 프로그램을 작성하시오.

<br/>

입력

표준 입력으로 다음 정보가 주어진다. 첫 번째 줄에는 점들의 개수를 나타내는 정수 N이 주어 진다. 다음 N개의 줄 각각에는 점의 좌표와 색깔을 나타내는 두 정수 x와 y가 주어진다.

<br/>

출력

표준 출력으로 모든 점에서 시작하는 화살표들의 길이 합을 출력한다.
 
<br/>
   
접근법

졍렬 후 가장 가까운 원소는 자신의 양 옆 중에서 구한다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();
    
    static int N;
    static ArrayList<Integer>[] a;
    
    static void input() {
        N = scan.nextInt();
        a = new ArrayList[N + 1];
        for (int color = 1; color <= N; color++) {
            a[color].add(coord);
        }
    }
    
    static int toLeft(int color, int idx) {
        if (idx == 0) {
            return Integer.MAX_VALUE;
        }
        return a[color].get(idx) - a[color].get(idx - 1);
    }

    static int toRight(int color, int idx) {
        if (idx + 1 == a[color].size()) {
            return Integer.MAX_VALUE;
        }
        return a[color].get(idx + 1) - a[color].get(idx);
    }
    
    static void pro() {
        for (int color = 1; color <= N; color++)
            Collections.sort(a[color]);
        
        int ans = 0;

        for (int color = 1; color <= N; color++) {
            for (int i = 0; i < a[color].size(); i++) {
                int left_distance = toLeft(color, i);
                int right_distance = toRight(color, i);
                ans += Math.min(left_distance, right_distance);
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

[BOJ 문제](https://www.acmicpc.net/problem/15970)