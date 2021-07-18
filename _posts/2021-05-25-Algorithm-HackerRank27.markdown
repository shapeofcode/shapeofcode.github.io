---
layout: post
title:  "HackerRank - Castle on the Grid"
date:   2021-05-25
last_modified_at: 2021-05-25
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Stack and Queues

<br/>

문제 설명 간략 :    

open(.) close(X)로 구성된 grid가 주어지고 출발점(x,y)와 도착점 (x,y)가 주어진다.

grid 끝지점과 장애물이 나올때 까지 움직 일 수 있으며, 도착점까지 움직이는데 최소 스텝수를 구하여라.


<br/>

제약사항

- 1 <= n <= 100
- 0 <= startX, startY, goalX, goalY <= n

<br/>

idea 

1. 출발 점에서 step별로 갈 수 있는 위치에 값을 표기하며 지도를 확장해나간다.
2. 목표지점에 도착하면 step을 리턴한다.
   

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
     * Complete the 'minimumMoves' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts following parameters:
     *  1. STRING_ARRAY grid
     *  2. INTEGER startX
     *  3. INTEGER startY
     *  4. INTEGER goalX
     *  5. INTEGER goalY
     */

    static int minimumMoves(List<String> grid, int startX, int startY, int goalX, int goalY){
        int[][] map = new int[grid.size()][grid.get(0).length()];
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid.get(0).length(); j++) {
                map[i][j] = grid.get(i).charAt(j) == '.' ? -1 : -2;
            }
        }
        map[startX][startY] = 0;
        int step = 0;
        while (true) {
            step++;
            for (int i = 0; i < map.length; i++) {
                for (int j = 0; j < map[0].length; j++) {
                    if (map[i][j] == -1) {
                        expandMap(map, i, j, step);
                        if (i == goalX && j == goalY && map[i][j] != -1) {
                            return step;
                        }
                    }
                }
            }
        }
    }

    private static void expandMap(int[][] map, int x, int y, int step) {
        // left
        for (int j = y - 1; j > -1 && map[x][j] != -2; j--) {
            if (map[x][j] == step - 1) {
                map[x][y] = step;
            }
        }

        // right
        for (int j = y + 1; j < map[0].length && map[x][j] != -2; j++) {
            if (map[x][j] == step - 1) {
                map[x][y] = step;
            }
        }
        // up
        for (int i = x - 1; i > -1 && map[i][y] != -2; i--) {
            if (map[i][y] == step - 1) {
                map[x][y] = step;
            }
        }

        // down
        for (int i = x + 1; i < map.length && map[i][y] != -2; i++) {
            if (map[i][y] == step - 1) {
                map[x][y] = step;
            }
        }
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = Integer.parseInt(bufferedReader.readLine().trim());

        List<String> grid = IntStream.range(0, n).mapToObj(i -> {
            try {
                return bufferedReader.readLine();
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        })
                .collect(toList());

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int startX = Integer.parseInt(firstMultipleInput[0]);

        int startY = Integer.parseInt(firstMultipleInput[1]);

        int goalX = Integer.parseInt(firstMultipleInput[2]);

        int goalY = Integer.parseInt(firstMultipleInput[3]);

        int result = Result.minimumMoves(grid, startX, startY, goalX, goalY);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/castle-on-the-grid/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=stacks-queues)