---
layout: post
title:  "HackerRank - New Year Chaos"
date:   2021-05-12
last_modified_at: 2021-05-12
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Arrays

<br/>

문제 설명 간략 : 1부터 n까지 구성된 list 가 주어지고 q는 각각의 위치가 표시된 최종 상태이다. 
각 원소는 최대 2번 자신의 앞에 수 와 swap 할 수 있고 최소 swap 수를 구하여라. 2번이 넘어가면
Too chaotic을 출력하라.

<br/>

제약사항

- 1 <= t <= 10
- 1 <= n <= 10^5

<br/>

idea 

1. 앞사람과 바꿀 수 있기 떄문에 뒤에서 부터 계산했을 때 그 자릿수의 값을 뺀게 2가 넘어가면 바꿀 수 없다.
2. 1번을 제외하고는 결국 자신의 두칸 앞자리 까지 바꿔야하는 수를 더해주면 된다.

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
     * Complete the 'minimumBribes' function below.
     *
     * The function accepts INTEGER_ARRAY q as parameter.
     */

    public static void minimumBribes(List<Integer> q) {
        // Write your code here
        int brides = 0;
        boolean chaotic = false;
        String result = "Too chaotic";
        for(int i = q.size() - 1; i >= 0; i--) {
            if(q.get(i) - (i+1) > 2) {
                chaotic = true;
                break;
            }
            for(int j = Math.max(0, q.get(i) - 2); j < i; j++) {
                if(q.get(j) > q.get(i)) {
                    brides++;
                }
            }
        }
        if(!chaotic) {
            result = Integer.toString(brides);
        }
        System.out.println(result);
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(bufferedReader.readLine().trim());

        IntStream.range(0, t).forEach(tItr -> {
            try {
                int n = Integer.parseInt(bufferedReader.readLine().trim());

                List<Integer> q = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                        .map(Integer::parseInt)
                        .collect(toList());

                Result.minimumBribes(q);
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        });

        bufferedReader.close();
    }
}

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/new-year-chaos/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=arrays)