---
layout: post
title:  "HackerRank - Fraudulent Activity Notifications"
date:   2021-05-18
last_modified_at: 2021-05-18
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Sorting

<br/>

문제 설명 간략 :  지출이 적힌 배열과 감시일자가 주어진다. d+1일의 지출이 이전 d일 동안의 중간값*2보다 크면
알림을 보낸다. 보내는 총 알림의 수를 구하여라. (d가 짝수일때는 중간값 두개의 평균을 기준으로 하고 홀수 일때는 중간 값으로 한다.)

<br/>

제약사항

- 1 <= n <= 2*10^5
- 1 <= d <= n
- 0 <= expenditure[i] <= 200

<br/>

idea 

1. 일반적인 sorting 함수로는 time limits이 걸린다.
2. 제약 조건을 활용하여 counting sort로 시간을 줄인다.
   

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
     * Complete the 'activityNotifications' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER_ARRAY expenditure
     *  2. INTEGER d
     */

    public static int activityNotifications(List<Integer> expenditure, int d) {

        int[] arr = expenditure.stream().mapToInt(i->i).toArray();
        int[] data = new int[201];
        for(int k = 0; k < d; k++) {
            data[arr[k]]++;
        }

        int noti = 0;

        boolean even = (d%2 == 0) ? true : false;

        for(int i = d; i < arr.length; i++) {

            double mid = 0.0;
            if(even) {

                Integer first = null;
                Integer second = null;
                int count = 0;
                for(int j = 0; j < data.length; j++) {
                    count += data[j];
                    if(first == null && count >= d/2) {
                        first = j;
                    }
                    if(second == null && count >= d/2+1) {
                        second = j;
                        break;
                    }
                }
                mid = (first+second)/2.0;
            } else {
                int count = 0;
                for(int j = 0; j < data.length; j++) {
                    count += data[j];
                    if(count > d/2) {
                        mid = j;
                        break;
                    }
                }
            }

            if(mid*2 <= arr[i]) {
                noti++;
            }

            data[arr[i]]++;
            data[arr[i-d]]--;
        }

        return noti;

    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int n = Integer.parseInt(firstMultipleInput[0]);

        int d = Integer.parseInt(firstMultipleInput[1]);

        List<Integer> expenditure = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                .map(Integer::parseInt)
                .collect(toList());

        int result = Result.activityNotifications(expenditure, d);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/fraudulent-activity-notifications/problem)