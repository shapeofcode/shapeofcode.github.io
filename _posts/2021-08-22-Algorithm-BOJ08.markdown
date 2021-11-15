---
layout: post
title:  "BOJ - 암호 만들기"
date:   2021-08-22
last_modified_at: 2021-08-22
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 128MB

<br/>

문제 유형 : 완전탐색

<br/>

문제 설명 간략 :    

암호는 서로 다른 L개의 알파벳 소문자들로 구성되며 최소 한 개의 모음(a, e, i, o, u)과 최소 두 개의 자음으로 구성되어 있다고 알려져 있다.
또한 정렬된 문자열을 선호하는 조교들의 성향으로 미루어 보아 암호를 이루는 알파벳이 암호에서 증가하는 순서로 배열되었을 것이라고 추측된다.
새 보안 시스템에서 조교들이 암호로 사용했을 법한 문자의 종류는 C가지가 있다고 한다. 
이 알파벳을 입수한 민식, 영식 형제는 조교들의 방에 침투하기 위해 암호를 추측해 보려고 한다. 
C개의 문자들이 모두 주어졌을 때, 가능성 있는 암호들을 모두 구하는 프로그램을 작성하시오.

<br/>

입력

첫째 줄에 두 정수 L, C가 주어진다. (3 ≤ L ≤ C ≤ 15) 다음 줄에는 C개의 문자들이 공백으로 구분되어 주어진다. 
주어지는 문자들은 알파벳 소문자이며, 중복되는 것은 없다.

<br/>

출력

각 줄에 하나씩, 사전식으로 가능성 있는 암호를 모두 출력한다.

<br/>
   
접근법

L 크기의 배열을 구성하여 index로 C에서 사용할 원소들을 선택한다. 
최소 한 개의 모음(a, e, i, o ,u)와 2개의 자음이 나온다면 출력.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();
    
    static void input() {
        M = scan.nextInt();
        N = scan.nextInt();
        chars = new char[N + 1];
        selected = new int[M + 1];
        String[] tokens = scan.nextLine().split(" ");
        for(int i = 1; i <= N; i++) {
            chars[i] = tokens[i - 1].charAt(0);
        }
    }
    
    static int N, M;
    static char[] chars;
    static int[] selected;
    
    static boolean isVowel(char x) {
        return x == 'a' || x == 'e' || x == 'i' || x == 'o' || x == 'u';    
    }
    
    static void rec_func(int k) {
        if (k == M + 1) {
            int vowel = 0, consonant = 0;
            for (int i = 1; i <= M; i++) {
                if (isVowel(chars[selected[i]])) vowel++;
                else consonant++;
            }
            if (vowel >= 1 && consonant >= 2) {
                for (int i = 1; i <= M; i++) sb.append(chars[selected[i]]);
                sb.append('\n');
            }
        } else {
            for (int cand = selected[k - 1] + 1; cand <= N; cand++) {
                selected[k] = cand;
                rec_func(k + 1);
                selected[k] = 0;
            }
        }
    }
    
    public static void main(String[] args) {
        input();
        
        Arrays.sort(chars, 1, N + 1);
        rec_func(1);
        System.out.println(sb.toString());
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

[BOJ 문제](https://www.acmicpc.net/problem/1759)