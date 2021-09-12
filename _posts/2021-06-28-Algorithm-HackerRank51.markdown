---
layout: post
title:  "HackerRank - Recursion: Davis' Staircase"
date:   2021-06-28
last_modified_at: 2021-06-28
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Recursion

<br/>

문제 설명 간략 :    

Davis는 집에 1,2 또는 3칸을 오를 수 있는 계단이 있다. 꼭대기까지 갈 수 있는 경우의 수를 구하여라. 


<br/>

제약사항

- 1 <= s <= 5
- 1 <= n <= 36

<br/>
   

<br/>

### 자바 풀이

```java
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;

class Result {

    /*
     * Complete the 'stepPerms' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts INTEGER n as parameter.
     */
    public static HashMap<Integer,Integer> memoization = new HashMap<Integer,Integer>();

    public static void setInit() {
        memoization.put(1,1);
        memoization.put(2,2);
        memoization.put(3,4);
    }
    public static int stepPerms(int n) {

        if(memoization.containsKey(n)) {
            return memoization.get(n);
        }

        int steps = stepPerms(n-1)+stepPerms(n-2)+stepPerms(n-3);

        memoization.put(n,steps);

        return memoization.get(n);

    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int s = Integer.parseInt(bufferedReader.readLine().trim());

        IntStream.range(0, s).forEach(sItr -> {
            try {
                int n = Integer.parseInt(bufferedReader.readLine().trim());

                Result.setInit();

                int res = Result.stepPerms(n);

                bufferedWriter.write(String.valueOf(res));
                bufferedWriter.newLine();
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        });

        bufferedReader.close();
        bufferedWriter.close();
    }
}



```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/ctci-recursive-staircase/problem)