---
layout: post
title:  "HackerRank - Sparse Arrays"
date:   2021-06-09
last_modified_at: 2021-06-09
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Data Structures - Arrays

<br/>

문제 설명 간략 :    

string 배열과 쿼리 string 배열이 주어진다. 쿼리 string 기준으로 string 배열에 몇번 나오는지 
count를 구해서 배열로 return해라.

<br/>

idea

loop를 돌면서 같은 값이 있는지 확인.

<br/>

제약사항

- 1 <= n <= 1000
- 1 <= q <= 1000
- 1 <= |strings[i],|queries[i]| <= 20

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
     * Complete the 'matchingStrings' function below.
     *
     * The function is expected to return an INTEGER_ARRAY.
     * The function accepts following parameters:
     *  1. STRING_ARRAY strings
     *  2. STRING_ARRAY queries
     */

    public static List<Integer> matchingStrings(List<String> strings, List<String> queries) {

        List<Integer> countList = new ArrayList<Integer>();

        for(int i = 0; i < queries.size(); i++) {
            int count = 0;
            String q = queries.get(i);

            for(int j = 0; j < strings.size(); j++) {
                if(q.equals(strings.get(j))) {
                    count++;
                }
            }

            countList.add(count);
        }

        return countList;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int stringsCount = Integer.parseInt(bufferedReader.readLine().trim());

        List<String> strings = IntStream.range(0, stringsCount).mapToObj(i -> {
                    try {
                        return bufferedReader.readLine();
                    } catch (IOException ex) {
                        throw new RuntimeException(ex);
                    }
                })
                .collect(toList());

        int queriesCount = Integer.parseInt(bufferedReader.readLine().trim());

        List<String> queries = IntStream.range(0, queriesCount).mapToObj(i -> {
                    try {
                        return bufferedReader.readLine();
                    } catch (IOException ex) {
                        throw new RuntimeException(ex);
                    }
                })
                .collect(toList());

        List<Integer> res = Result.matchingStrings(strings, queries);

        bufferedWriter.write(
                res.stream()
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

[해커랭크 문제](https://www.hackerrank.com/challenges/sparse-arrays/problem)