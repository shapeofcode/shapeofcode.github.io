---
layout: post
title:  "BOJ - 단어정렬"
date:   2021-08-30
last_modified_at: 2021-08-30
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 256MB

<br/>

문제 유형 : 정렬

<br/>

문제 설명 간략 :    

알파벳 소문자로 이루어진 N개의 단어가 들어오면 아래와 같은 조건에 따라 정렬하는 프로그램을 작성하시오.

1.길이가 짧은 것부터
2.길이가 같으면 사전 순으로

<br/>

입력

첫째 줄에 단어의 개수 N이 주어진다. (1 ≤ N ≤ 20,000) 둘째 줄부터 N개의 줄에 걸쳐 알파벳 소문자로 이루어진 단어가 한 줄에 하나씩 주어진다. 주어지는 문자열의 길이는 50을 넘지 않는다.

<br/>

출력

조건에 따라 정렬하여 단어들을 출력한다. 단, 같은 단어가 여러 번 입력된 경우에는 한 번씩만 출력한다.
 
<br/>
   
접근법

Comparator로 구현

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();
    
    static class MyComparator implements Comparator<String> {
        @Override
        public int compare(String lhs, String rhs) {
            if (lhs.length() != rhs.length())
                return lhs.length() - rhs.length();
            return lhs.compareTo(rhs);
        }
    }
    
    static int N;
    static String[] a;
    
    static void input() {
        N = scan.nextInt();
        a = new String[N];
        for (int i = 0; i < N; i++) {
            a[i] = scan.next();
        }
    }
    
    static void pro() {
        Arrays.sort(a, new MyComparator());
        for (int i = 0; i < N; i++) {
            if(i == 0 || a[i].compareTo(a[i - 1]) != 0)
                sb.append(a[i]).append('\n');
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

[BOJ 문제](https://www.acmicpc.net/problem/1181)