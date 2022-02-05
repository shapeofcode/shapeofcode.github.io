---
layout: post
title:  "BOJ - 고냥이"
date:   2022-02-06
last_modified_at: 2022-02-06
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 1초

메모리제한 512MB

<br/>

문제 유형 : 두 포인터

<br/>

문제 설명 간략 :    

고양이는 너무 귀엽다. 사람들은 고양이를 너무 귀여워했고, 
결국 고양이와 더욱 가까워지고 싶어 고양이와의 소통을 위한 고양이 말 번역기를 발명하기로 했다. 
이 번역기는 사람의 언어를 고양이의 언어로, 고양이의 언어를 사람의 언어로 바꾸어 주는 희대의 발명품이 될 것이다.

현재 고양이말 번역기의 베타버전이 나왔다. 
그러나 이 베타버전은 완전 엉망진창이다. 
베타버전의 번역기는 문자열을 주면 그 중에서 최대 N개의 종류의 알파벳을 가진 연속된 문자열밖에 인식하지 못한다. 
굉장히 별로지만 그나마 이게 최선이라고 사람들은 생각했다. 
그리고 문자열이 주어졌을 때 이 번역기가 인식할 수 있는 최대 문자열의 길이는 얼마인지가 궁금해졌다.

고양이와 소통할 수 있도록 우리도 함께 노력해보자.

<br/>

입력

첫째 줄에는 인식할 수 있는 알파벳의 종류의 최대 개수 N이 입력된다. (1 < N ≤ 26)

둘째 줄에는 문자열이 주어진다. (1 ≤ 문자열의 길이 ≤ 100,000) 단, 문자열에는 알파벳 소문자만이 포함된다.

<br/>

출력

첫째 줄에 번역기가 인식할 수 있는 문자열의 최대길이를 출력한다.

<br/>
   
접근법

최소, 최대를 빠르게 알기 위해 정렬하고 투 포인터를 이용해 양 끝 지점의 합이 타겟보타 클 경우 오른쪽 감소,
같을 경우는 true 그 외에는 왼쪽을 증가 시키며 왼쪽이 오른쪽보다 커질 때까지 합으로 표현된 값이 없을 경우 false를 반환한다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();

    static int N, kind;
    static String A;
    static int[] cnt;

    static void input() {
        N = scan.nextInt();
        A = scan.nextLine();
        cnt = new int[26];
    }

    static void add(char x) {
        cnt[x - 'a']++;
        if (cnt[x - 'a'] == 1) {
            kind++;
        }
    }
    
    static void erase(char x) {
        cnt[x - 'a']--;
        if(cnt[x-'a'] == 0) {
            kind--;
        }
    }
    
    static void pro() {
        int len = A.length(), ans = 0;
        for (int R = 0, L =0; R < len; R++) {
            add(A.charAt(R));
            
            while(kind > N) {
                erase(A.charAt(L++));
            }
            
            ans = Math.max(ans, R - L + 1);
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

[BOJ 문제](https://www.acmicpc.net/problem/16472)