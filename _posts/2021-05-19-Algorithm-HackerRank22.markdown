---
layout: post
title:  "HackerRank - Luck Balance"
date:   2021-05-19
last_modified_at: 2021-05-19
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Easy

<br/>

문제 유형 : Greedy

<br/>

문제 설명 간략 :  n개의 contest와 중요한 contest를 k번 이상 지면 안되는 
input이 주이지고 contest에 승리하면 L[i] 만큼 운이 줄어들고 지면 L[i] 만큼 운이 늘어난다. 

T[i]는 contest가 중요한지 안중요한지 1과 0으로 표기한다.

maximum luck을 구하여라.

<br/>

제약사항

- 1 <= n <= 100
- 0 <= k <= N
- 1 <= L[i] <= 10^4
- T[i] 는 {0,1} 중 하나이다.

<br/>

idea 

1. 전체 패배한 경우에서 중요한 경기 중 최소 이겨야하는 경기 수를 구해서 빼준다.
   

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
     * Complete the 'luckBalance' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER k
     *  2. 2D_INTEGER_ARRAY contests
     */

    public static int luckBalance(int k, List<List<Integer>> contests) {
        // Write your code here
        int result = 0;

        List<Integer> lucks = new ArrayList<Integer>();

        for(int i = 0; i < contests.size(); i++) {
            int luck = contests.get(i).get(0);
            int imptnt = contests.get(i).get(1);

            result += luck;

            if(imptnt == 1) {
                lucks.add(luck);
            }
        }

        Collections.sort(lucks);

        int wins = lucks.size()-k;
        if(wins > 0) {
            for(int j = 0;  j < wins; j++) {
                result -= lucks.get(j)*2;
            }
        }

        return result;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int n = Integer.parseInt(firstMultipleInput[0]);

        int k = Integer.parseInt(firstMultipleInput[1]);

        List<List<Integer>> contests = new ArrayList<>();

        IntStream.range(0, n).forEach(i -> {
            try {
                contests.add(
                        Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                                .map(Integer::parseInt)
                                .collect(toList())
                );
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        });

        int result = Result.luckBalance(k, contests);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/luck-balance/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=greedy-algorithms)