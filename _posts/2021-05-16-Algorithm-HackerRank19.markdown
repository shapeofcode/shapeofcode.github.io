---
layout: post
title:  "HackerRank - Frequency Queries"
date:   2021-05-16
last_modified_at: 2021-05-16
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Dictionaries and Hashmaps

<br/>

문제 설명 간략 :  q라는 quries들이 주어지고 1 x일 경우 x를 insert,
2 y일 경우 y를 delete,
3 z일 경우 빈도가 z 값일 경우 1을 출력 아닐경우 0을 출력한다.

<br/>

제약사항

- 1 <= q <= 10^5
- 1 <= x,y,z <= 10^9
- All queries[i][0] 은 {1,2,3} 중 하나
- 1 < queries[i][1] <= 10^9

<br/>

idea 

1. 1이면 추가하고 2면 빼는 map을 구성한다. 3이 나오면 해당 빈도수 만큼 나온 값이 있는지 확인한다.
2. 그냥 풀 경우 time limit이 걸린다. 배열을 선언하여 배열 인덱스(빈도수)에 값(갯수)으로 표기하여 탐색 시간을 줄인다. 
   

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

public class Solution {

  // Complete the freqQuery function below.
  static List<Integer> freqQuery(List<int[]> queries) {

    List<Integer> result = new ArrayList<Integer>();

    Map<Integer,Integer> map = new HashMap<Integer,Integer>();
    int size = queries.size();
    int[] freqOcr = new int[size + 1];

    for(int i = 0; i < size; i++) {
      int [] query = queries.get(i);
      int operation = query[0];
      int data = query[1];

      if(operation == 1) {
        int count = map.containsKey(data) ? map.get(data) : 0;
        map.put(data, count+1);
        freqOcr[count]--;
        freqOcr[count+1]++;
      }else if(operation == 2) {
        int count = map.containsKey(data) ? map.get(data) : 0;
        if(count > 0) {
          map.put(data, count-1);
          freqOcr[count]--;
          freqOcr[count-1]++;
        }
      }else {
        if(data > freqOcr.length) {
          result.add(0);
        }else {
          result.add(freqOcr[data] > 0 ? 1 : 0);
        }
      }
    }

    return result;

  }

  public static void main(String[] args) throws IOException {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
    BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

    int q = Integer.parseInt(bufferedReader.readLine().trim());
    List<int[]> queries = new ArrayList<>();

    for(int i=0; i<q; i++){
      String[] row = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");
      int cmd = Integer.parseInt(row[0]);
      int v = Integer.parseInt(row[1]);
      int[] query = new int[2];
      query[0] = cmd;
      query[1] = v;
      queries.add(query);
    }

    List<Integer> ans = freqQuery(queries);

    bufferedWriter.write(
            ans.stream()
                    .map(Object::toString)
                    .collect(joining("\n"))
                    + "\n"
    );

    bufferedReader.close();
    bufferedWriter.close();
  }
}




```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/frequency-queries/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dictionaries-hashmaps)