---
layout: post
title:  "BOJ - 단어정렬"
date:   2021-08-31
last_modified_at: 2021-08-31
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 3초

메모리제한 1024MB

<br/>

문제 유형 : 정렬

<br/>

문제 설명 간략 :    

- 파일을 확장자 별로 정리해서 몇 개씩 있는지 알려줘
- 보기 편하게 확장자들을 사전 순으로 정렬해 줘

<br/>

입력

첫째 줄에 바탕화면에 있는 파일의 개수 N이 주어진다. (1 <= N <= 50000)

둘째 줄부터 N개 줄에 바탕화면에 있는 파일의 이름이 주어진다. 파일의 이름은 알파벳 소문자와 점(.)으로만 구성되어 있다. 점은 정확히 한 번 등장하며, 
파일 이름의 첫 글자 또는 마지막 글자로 오지 않는다. 각 파일의 이름의 길이는 최소 3, 최대 100이다.

<br/>

출력

확장자의 이름과 그 확장자 파일의 개수를 한 줄에 하나씩 출력한다. 확장자가 여러 개 있는 경우 확장자 이름의 사전순으로 출력한다.
 
<br/>
   
접근법

확장자 짤라서 정렬 후 카운트

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();
    
    static int N;
    static String[] a;
    
    static void input() {
        N = scan.nextInt();
        a = new String[N+1];
        for (int i = 1; i <= N; i++) {
            a[i] = scan.nextLine().split("\\.")[1];
        }
    }
    
    static void pro() {
        Arrays.sort(a, 1, N + 1);
        
        for (int i = 1; i <= N;) {
            int cnt = 1, j = i + 1;
            for(; j <= N; j++){
                if (a[j].compareTo(a[i]) == 0) cnt++;
                else break;
            }
            
            sb.append(a[i]).append(' ').append(cnt).append('\n');
            i = j;
        }
        System.out.println(sb.toString());
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

[BOJ 문제](https://www.acmicpc.net/problem/20291)