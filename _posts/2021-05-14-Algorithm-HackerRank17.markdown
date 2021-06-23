---
layout: post
title:  "HackerRank - Common Child"
date:   2021-05-14
last_modified_at: 2021-05-14
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : String Manipulation

<br/>

문제 설명 간략 : 같은 길이의 두 문자열이 주어지고 공통된 가장 긴 문자열을 구하여라.

<br/>

제약사항

- 1 <= |s1|, |s2| <= 5000 (s의 길이)

<br/>

idea 

1. 각 문자열을 char matrix로 표현하여 각 substring의 특징은 
   두 행렬 값이 같으면 대각선[i-1,j-1] 값의 +1이 해당 matrix의 값이며
   다르면 옆[i-1][j] 위[i][j-1] 값 중 최대값이 matrix값이 된다.
   그리고 matrix 마지막 값이 총 길이가 되며 뒤로 따라가면 공통된 값
   즉, 가장 긴 문자열이 나온다.
   

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
     * Complete the 'commonChild' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts following parameters:
     *  1. STRING s1
     *  2. STRING s2
     */

    public static int commonChild(String s1, String s2) {
        // Write your code here

        int C [][] = new int[s1.length()+1][s2.length()+1];

        for(int i = 1; i < s1.length()+1; i++) {
            for(int j = 1; j < s2.length()+1; j++) {
                if(s1.charAt(i-1) == s2.charAt(j-1)) {
                    C[i][j] = C[i-1][j-1]+1;
                } else {
                    C[i][j] = Math.max(C[i-1][j], C[i][j-1]);
                }
            }
        }

        return C[s1.length()][s2.length()];
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String s1 = bufferedReader.readLine();

        String s2 = bufferedReader.readLine();

        int result = Result.commonChild(s1, s2);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}


```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/common-child/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=strings)