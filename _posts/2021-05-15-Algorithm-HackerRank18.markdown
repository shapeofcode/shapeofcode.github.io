---
layout: post
title:  "HackerRank - Sherlock and Anagrams"
date:   2021-05-15
last_modified_at: 2021-05-15
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Dictionaries and Hashmaps

<br/>

문제 설명 간략 : 문자가 주어지고 만들 수 있는 substring의 anagram 쌍의 갯수를 구하여라 

<br/>

제약사항

- 1 <= q <= 10
- 2 <= length of s <= 100
  (s는 알파벳 소문자로만 구성된다.)

<br/>

idea 

1. anagram 특성을 고려한다.(길이가 같아야하며, 구성된 문자열이 같아야한다.)
2. 부분문자열을 sorting하여 map에 담아둠으로써 anagram으로 만들 수 있는 쌍의 갯수를 구할 수 있다.
3. 쌍은 구성된 map의 갯수에서 두개를 뽑아 만들 수 있다. <sub>n</sub>C<sub>2</sub> -> n(n-1)/2
   

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
    * Complete the 'sherlockAndAnagrams' function below.
    *
    * The function is expected to return an INTEGER.
    * The function accepts STRING s as parameter.
    */

   public static int sherlockAndAnagrams(String s) {

      int result = 0;

      int sLength = s.length();
      int idx = 1;

      while(idx < sLength) {
         Map<String,Integer> map = new HashMap<String,Integer>();

         for(int i = 0; i <= s.length()-idx; i++) {
            String sub = s.substring(i,i+idx);
            char [] c = sub.toCharArray();
            Arrays.sort(c);
            String sorted = String.valueOf(c);
            int count = map.getOrDefault(sorted, 0);
            map.put(sorted, count + 1);
         }

         Iterator<String> keys = map.keySet().iterator();
         while( keys.hasNext() ){
            String key = keys.next();
            int count = map.get(key);
            result += count*(count-1)/2;
         }

         idx++;
      }

      return result;

   }

}

public class Solution {
   public static void main(String[] args) throws IOException {
      BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
      BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

      int q = Integer.parseInt(bufferedReader.readLine().trim());

      IntStream.range(0, q).forEach(qItr -> {
         try {
            String s = bufferedReader.readLine();

            int result = Result.sherlockAndAnagrams(s);

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

[해커랭크 문제](https://www.hackerrank.com/challenges/sherlock-and-anagrams/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=dictionaries-hashmaps)