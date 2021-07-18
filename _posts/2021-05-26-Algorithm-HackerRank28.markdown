---
layout: post
title:  "HackerRank - Roads and Libraries"
date:   2021-05-26
last_modified_at: 2021-05-26
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Graphs

<br/>

문제 설명 간략 :    

도시에 도서관과 도로를 설치하여 모든 시민이 도서관을 방문할 수 있는 최소 비용을 구하여라.


<br/>

제약사항

- 1 <= q <= 100
- 1 <= n <= 10^5
- 0 <= m <= min(10^5, n*(n-1)/2)
- 1 <= c_road_, c_lib <= 10^5
- 1 <= u[i], v[i] <=n

<br/>

idea 

1. 도시별 방문 횟수는 도시별 도서관 수 또는 도시간의 연결하는 도로의 개수로 사용
   

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
     * Complete the 'roadsAndLibraries' function below.
     *
     * The function is expected to return a LONG_INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER n - number ofcities
     *  2. INTEGER c_lib - cost of library
     *  3. INTEGER c_road - cost of road
     *  4. 2D_INTEGER_ARRAY cities - can be connected between cities
     */

    public static long roadsAndLibraries(int n, int c_lib, int c_road, List<List<Integer>> cities) {

        List<ArrayList<Integer>> graph = initGraph(n, cities);
        boolean[] visited = new boolean[n];

        long cost = 0;

        for(int i = 0; i < graph.size(); i++) {
            if(!visited[i]) {
                if(c_lib > c_road) {
                    cost += c_lib + (c_road * (visitedCount(i, visited, graph) -1));
                } else {
                    cost += c_lib * visitedCount(i, visited, graph);
                }
            }
        }

        return cost;
    }

    static List<ArrayList<Integer>> initGraph(int n, List<List<Integer>> cities) {
        List<ArrayList<Integer>> graph = new ArrayList<>();

        for(int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        for(int i = 0; i < cities.size(); i++) {
            graph.get(cities.get(i).get(0) - 1).add(cities.get(i).get(1) -1);
            graph.get(cities.get(i).get(1) - 1).add(cities.get(i).get(0) -1);
        }

        return graph;
    }

    static long visitedCount(int index, boolean[] visited, List<ArrayList<Integer>> graph) {
        long count = 1;
        visited[index] = true;

        for(int i = 0; i < graph.get(index).size(); i++) {
            if(!visited[graph.get(index).get(i)]) {
                count += visitedCount(graph.get(index).get(i), visited, graph);
            }
        }

        return count;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int q = Integer.parseInt(bufferedReader.readLine().trim());

        IntStream.range(0, q).forEach(qItr -> {
            try {
                String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

                int n = Integer.parseInt(firstMultipleInput[0]);

                int m = Integer.parseInt(firstMultipleInput[1]);

                int c_lib = Integer.parseInt(firstMultipleInput[2]);

                int c_road = Integer.parseInt(firstMultipleInput[3]);

                List<List<Integer>> cities = new ArrayList<>();

                IntStream.range(0, m).forEach(i -> {
                    try {
                        cities.add(
                                Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
                                        .map(Integer::parseInt)
                                        .collect(toList())
                        );
                    } catch (IOException ex) {
                        throw new RuntimeException(ex);
                    }
                });

                long result = Result.roadsAndLibraries(n, c_lib, c_road, cities);

                bufferedWriter.write(String.valueOf(result));
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

[해커랭크 문제](https://www.hackerrank.com/challenges/torque-and-development/problem?h_l=interview&isFullScreen=true&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=graphs)