---
layout: post
title:  "BOJ - 연산자 끼워넣기"
date:   2021-08-19
last_modified_at: 2021-08-19
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

시간제한 : 2초

메모리제한 512MB

<br/>

문제 유형 : 완전탐색

<br/>

문제 설명 간략 :    

N개의 수로 이루어진 수열 A1, A2, ..., AN이 주어진다. 또, 수와 수 사이에 끼워넣을 수 있는 N-1개의 연산자가 주어진다. 연산자는 덧셈(+), 뺄셈(-), 곱셈(×), 나눗셈(÷)으로만 이루어져 있다.

우리는 수와 수 사이에 연산자를 하나씩 넣어서, 수식을 하나 만들 수 있다. 이때, 주어진 수의 순서를 바꾸면 안 된다.


<br/>

입력

첫째 줄에 수의 개수 N(2 ≤ N ≤ 11)가 주어진다. 둘째 줄에는 A1, A2, ..., AN이 주어진다. (1 ≤ Ai ≤ 100) 
셋째 줄에는 합이 N-1인 4개의 정수가 주어지는데, 차례대로 덧셈(+)의 개수, 뺄셈(-)의 개수, 곱셈(×)의 개수, 나눗셈(÷)의 개수이다.

<br/>

출력

첫째 줄에 만들 수 있는 식의 결과의 최댓값을, 둘째 줄에는 최솟값을 출력한다. 연산자를 어떻게 끼워넣어도 
항상 -10억보다 크거나 같고, 10억보다 작거나 같은 결과가 나오는 입력만 주어진다. 또한, 앞에서부터 계산했을 때, 
중간에 계산되는 식의 결과도 항상 -10억보다 크거나 같고, 10억보다 작거나 같다.

<br/>
   
접근법

연산자를 배열에 담아두고  재귀호출로 값 할당.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Main {
    static FastReader scan = new FastReader();
    static StringBuilder sb = new StringBuilder();
    
    static void input() {
        N = scan.nextInt();
        nums = new int[N + 1];
        operators = new int[5];
        for (int i = 1; i <= N; i++) nums[i] = scan.nextInt();
        for (int i = 1; i <= 4; i++) operators[i] = scan.nextInt();
        
        max = Integer.MIN_VALUE;
        min = Integer.MAX_VALUE;
    }
    
    static int N, max, min;
    static int[] nums, operators;
    
    static int calculator(int operand1, int operator, int operand2) {
        if (operator == 1) {
            return operand1 + operand2;
        } else if (operator == 2) {
            return operand1 - operand2;
        } else if (operator == 3) {
            return operand1 * operand2;
        } else {
            return operand1 / operand2;
        }
    }
    
    static void rec_func(int k, int value) {
        if (k == N) {
            max = Math.max(max, value);
            min = Math.min(min, value);
        } else {
            for (int cand = 1; cand <= 4; cand++) {
                if (operators[cand] >= 1) {
                    operators[cand]--;
                    rec_func(k + 1, calculator(value, cand, nums[k + 1]));
                    operators[cand]++;
                }
            }
        }
    }
    
    public static void main(String[] args) {
        input();
        rec_func(1, nums[1]);
        sb.append(max).append('\n').append(min);
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

[BOJ 문제](https://www.acmicpc.net/problem/14888)