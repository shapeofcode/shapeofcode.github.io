---
layout: post
title:  "HackerRank - Simple Text Editor"
date:   2021-06-27
last_modified_at: 2021-06-27
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Data Structures - Stacks

<br/>

문제 설명 간략 :    

String S와 operation이 포함된 배열이 주어진다. 결과를 출력하라.

1.append(W) - Append string W to the end of S.
2.delete(k) - Delete the last k Characters of S.
3.print(k) - Print the k<sup>th</sup> character of S.
4.undo() - Undo the las(not previously undone) operation of type 1 or 2. reverting S to the state it was in prior th that
operation

<br/>

제약사항

- 1 <= Q <= 10^5
- 1 <= k <= |S|
- The sum of the lengths of all W in the input <= 10^6
- The sym of k over all delete operations <= 2*10^6
- All input characters are lowercase English letters.
- It is guaranteed that the sequence of operations given as input is possible to perform.

<br/>
   

<br/>

### 자바 풀이

```java
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {

        try {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

            Stack<String> history = new Stack<>();
            StringBuilder current = new StringBuilder();

            int count = Integer.parseInt(br.readLine());
            for (int i = 0; i < count; i++) {
                String line = br.readLine();
                String [] arr = line.split(" ");
                int operation = Integer.parseInt(arr[0]);

                switch (operation) {
                    case 1:
                        history.push(current.toString());
                        current.append(arr[1]);
                        break;
                    case 2:
                        history.push(current.toString());
                        current = new StringBuilder(current.substring(0, current.length() - Integer.parseInt(arr[1])));
                        break;
                    case 3:
                        System.out.println(current.charAt(Integer.parseInt(arr[1]) - 1));
                        break;
                    case 4:
                        current = new StringBuilder(history.pop());
                        break;
                }
            }
        }catch(Exception e) {
            System.out.println(e);
        }

    }
}



```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/simple-text-editor/problem)