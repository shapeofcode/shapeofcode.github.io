---
layout: post
title:  "HackerRank - Ice Cream Parlor"
date:   2021-05-02
last_modified_at: 2021-05-02
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Search

<br/>

문제 설명 간략 : 사용가능한 돈이 주어지고 아이스크림 비용이 선언된 배열이 주어진다. 두개의 조합을 선택하여 
비용을 모두 소진할 수 있는 배열의 인덱스+1 값을 구하라.


<br/>

제약사항

- 1 <= t <= 50
- 2 <= money <= 10^9
- 2 <= n <= 5*10^4
- 1 <= cost[i] <= 10^9

<br/>

idea 

1. 비용 배열을 돌면서 전체 금액에 필요한 두 조합을 찾는다.

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
     * Complete the 'whatFlavors' function below.
     *
     * The function accepts following parameters:
     *  1. INTEGER_ARRAY cost
     *  2. INTEGER money
     */

    public static void whatFlavors(List<Integer> cost, int money) {

        HashMap<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < cost.size(); i++){
            int target = money-cost.get(i);
            if(cost.get(i) < money){
                if(map.containsKey(target)){
                    System.out.println(map.get(target) + " " + (i+1));
                    break;
                } else {
                    map.put(cost.get(i), i+1);
                }
            }
        }

    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));

        int t = Integer.parseInt(bufferedReader.readLine().trim());

        IntStream.range(0, t).forEach(tItr -> {
            try {
                int money = Integer.parseInt(bufferedReader.readLine().trim());

                int n = Integer.parseInt(bufferedReader.readLine().trim());

                List<Integer> cost = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                        .map(Integer::parseInt)
                        .collect(toList());

                Result.whatFlavors(cost, money);
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

[해커랭크 문제](https://www.hackerrank.com/challenges/ctci-ice-cream-parlor/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=search)