---
layout: post
title:  "BOJ - 랜선 자르기"
date:   2022-01-24
last_modified_at: 2022-01-24
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 128MB

<br/>

문제 유형 : 이분탐색

<br/>

문제 설명 간략 :    

집에서 시간을 보내던 오영식은 박성원의 부름을 받고 급히 달려왔다. 
박성원이 캠프 때 쓸 N개의 랜선을 만들어야 하는데 너무 바빠서 영식이에게 도움을 청했다.

이미 오영식은 자체적으로 K개의 랜선을 가지고 있다. 그러나 K개의 랜선은 길이가 제각각이다. 
박성원은 랜선을 모두 N개의 같은 길이의 랜선으로 만들고 싶었기 때문에 K개의 랜선을 잘라서 만들어야 한다. 
예를 들어 300cm 짜리 랜선에서 140cm 짜리 랜선을 두 개 잘라내면 20cm는 버려야 한다. (이미 자른 랜선은 붙일 수 없다.)

편의를 위해 랜선을 자르거나 만들 때 손실되는 길이는 없다고 가정하며, 
기존의 K개의 랜선으로 N개의 랜선을 만들 수 없는 경우는 없다고 가정하자. 
그리고 자를 때는 항상 센티미터 단위로 정수길이만큼 자른다고 가정하자. 
N개보다 많이 만드는 것도 N개를 만드는 것에 포함된다. 
이때 만들 수 있는 최대 랜선의 길이를 구하는 프로그램을 작성하시오.

<br/>

입력

첫째 줄에는 오영식이 이미 가지고 있는 랜선의 개수 K, 그리고 필요한 랜선의 개수 N이 입력된다. 
K는 1이상 10,000이하의 정수이고, N은 1이상 1,000,000이하의 정수이다. 
그리고 항상 K ≦ N 이다. 그 후 K줄에 걸쳐 이미 가지고 있는 각 랜선의 길이가 센티미터 단위의 정수로 입력된다. 
랜선의 길이는 2^31-1보다 작거나 같은 자연수이다.

<br/>

출력

첫째 줄에 N개를 만들 수 있는 랜선의 최대 길이를 센티미터 단위의 정수로 출력한다.
 
<br/>
   
접근법

자르는 갯수의 합이 N개 이상에 부합하는 최대 길이의 랜선을 이분탐색으로 구한다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {

    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int K, N;
    static int[] A;

    static void input() {
        K = scan.nextInt();
        N = scan.nextInt();
        A = new int[K + 1];
        for(int i = 1; i <= K; i++) {
            A[i] = scan.nextInt();
        }
    }

    static boolean determination(long len) {
        long sum = 0;
        for(int i = 1; i <= K; i++) {
            sum += A[i] / len;
        }

        return sum >= N;
    }

    static void pro() {
        long L = 1, R = Integer.MAX_VALUE, ans = 0;

        while(L <= R) {
            long mid = (L + R) / 2;
            if(determination(mid)) {
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

[BOJ 문제](https://www.acmicpc.net/problem/1654)