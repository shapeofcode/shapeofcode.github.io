---
layout: post
title:  "HackerRank - Balanced Brackets"
date:   2021-05-09
last_modified_at: 2021-05-09
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Stacks and Queues

<br/>

문제 설명 간략 : (,), {,}, [,] 유형의 괄호가 주어진다. balanced된 괄호면 YES를 출력 unbalanced된 괄호면 NO를 출력한다.

<br/>

제약사항

- 1 <= n <= 10^3
- 1 <= |s| <= 10^3

<br/>

idea 

1. 괄호짝의 hashmap를 만들어 둔다.
2. Stack에 값을 보면서(peek) 일치하는게 있으면 pop 없으면 push
3. 최종 Stack이 비어있으면 balanced된 괄호이다.

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
     * Complete the 'isBalanced' function below.
     *
     * The function is expected to return a STRING.
     * The function accepts STRING s as parameter.
     */

    public static String isBalanced(String s) {

        Map<Character,Character> pairs = new HashMap<Character,Character>();
        pairs.put('}','{');
        pairs.put(']','[');
        pairs.put(')','(');

        Stack<Character> stack = new Stack<Character>();
        stack.push(s.charAt(0));
        for(int i = 1; i < s.length(); i++) {
            if(!stack.empty() && (pairs.get(s.charAt(i)) == stack.peek())) {
                stack.pop();
            } else {
                stack.push(s.charAt(i));
            }
        }

        String result = "NO";
        if(stack.empty()) {
            result = "YES";
        }

        return result;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int t = Integer.parseInt(bufferedReader.readLine().trim());

        IntStream.range(0, t).forEach(tItr -> {
            try {
                String s = bufferedReader.readLine();

                String result = Result.isBalanced(s);

                bufferedWriter.write(result);
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

[해커랭크 문제](https://www.hackerrank.com/challenges/angry-children/problem)