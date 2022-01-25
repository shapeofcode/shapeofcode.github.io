---
layout: post
title:  "BOJ - 어두운 굴다리"
date:   2022-01-25
last_modified_at: 2022-01-25
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 1초

메모리제한 512MB

<br/>

문제 유형 : 이분탐색

<br/>

문제 설명 간략 :    

인하대학교 후문 뒤쪽에는 어두운 굴다리가 있다.
겁쟁이 상빈이는 길이 조금이라도 어둡다면 가지 않는다.
따라서 굴다리로 가면 최단거리로 집까지 갈수 있지만, 굴다리는 어둡기 때문에 빙빙 돌아서 집으로 간다.
안타깝게 여긴 인식이는 굴다리 모든 길 0~N을 밝히게 가로등을 설치해 달라고 인천광역시에 민원을 넣었다.
인천광역시에서 가로등을 설치할 개수 M과 각 가로등의 위치 x들의 결정을 끝냈다.
그리고 각 가로등은 높이만큼 주위를 비출 수 있다.
하지만 갑자기 예산이 부족해진 인천광역시는 가로등의 높이가 높을수록 가격이 비싸지기 때문에
최소한의 높이로 굴다리 모든 길 0~N을 밝히고자 한다. 최소한의 예산이 들 높이를 구하자.
단 가로등은 모두 높이가 같아야 하고, 정수이다.



<br/>

입력

첫 번째 줄에 굴다리의 길이 N 이 주어진다. (1 ≤ N ≤ 100,000)

두 번째 줄에 가로등의 개수 M 이 주어진다. (1 ≤ M ≤ N)

다음 줄에 M 개의 설치할 수 있는 가로등의 위치 x 가 주어진다. (0 ≤ x ≤ N)

가로등의 위치 x는 오름차순으로 입력받으며 가로등의 위치는 중복되지 않으며, 정수이다.


<br/>

출력

굴다리의 길이 N을 모두 비추기 위한 가로등의 최소 높이를 출력한다.


<br/>
   
접근법

마지막 지점을 뺀값이 가로등 높이 안에 들어가지 않으면 길이를 늘리고 마지막 지점이 N보다 큰 조건의 가로등 최소 높이를 구한다.

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
        A = new int[M + 1];
        for (int i = 1; i <= M; i++) {
            A[i] = scan.nextInt();
        }
    }

    static boolean determination(int height) {
        int last = 0;  // 밝혀진 마지막 위치
        for (int i = 1; i <= M; i++) {
            if (A[i] - last <= height) {
                last = A[i] + height;
            } else {
                return false;
            }
        }
        return last >= N;
    }

    static void pro() {
        int L = 0, R = N, ans = N;

        Arrays.sort(A, 1, M + 1);
        // [L ... R] 범위 안에 정답이 존재한다!
        // 이분 탐색과 determination 문제를 이용해서 answer를 빠르게 구하자!
        while (L <= R) {
            int mid = (L + R) / 2;
            if (determination(mid)) {
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

[BOJ 문제](https://www.acmicpc.net/problem/13702)