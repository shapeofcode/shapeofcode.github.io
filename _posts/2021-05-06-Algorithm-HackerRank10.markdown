---
layout: post
title:  "HackerRank - Minimum Time Required"
date:   2021-05-06
last_modified_at: 2021-05-06
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Search

<br/>

문제 설명 간략 : 하나의 물건을 생산하는데 걸리는 날짜가 담긴 배열이 주어지고 기계는 동시에 돌아간다.
생산 목표치가 주어졌을 때 생산이 완료되는 날짜를 구하여라.

<br/>

제약사항

- 1 <= n <= 10^5
- 1 <= goal <= 10^9
- 1 <= machines[i] <= 10^9

<br/>

idea 

(처음에는 하루 씩 늘려가며 mod가 0인 값을 더해 주었다. 결과는 당연히 Time limit)

1. 배열을 정렬하여 제품 생산이 완료되는 최소 시간과 최대 시간을 구할 수 있다. (cost*goal)
2. 중간 값을 이용해 binary search를 통한 탐색을 최소화 한다.

<br/>

### 자바 풀이

```java
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.regex.*;

public class Solution {

    // Complete the minTime function below.
    static long minTime(long[] machines, long goal) {

        Arrays.sort(machines);

        long maxCost = machines[machines.length-1];
        long minTime = machines[0];
        long maxTime = maxCost*goal;

        while(minTime < maxTime) {
            long middle = (minTime+maxTime)/2;
            long cost = 0;
            for(long machine : machines) {
                cost += middle/machine;
            }
            if(cost < goal) {
                minTime = middle+1;
            } else {
                maxTime = middle;
            }
        }

        return minTime;

    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] nGoal = scanner.nextLine().split(" ");

        int n = Integer.parseInt(nGoal[0]);

        long goal = Long.parseLong(nGoal[1]);

        long[] machines = new long[n];

        String[] machinesItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < n; i++) {
            long machinesItem = Long.parseLong(machinesItems[i]);
            machines[i] = machinesItem;
        }

        long ans = minTime(machines, goal);

        bufferedWriter.write(String.valueOf(ans));
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/minimum-time-required/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=search)