---
layout: post
title:  "HackerRank - Sorting: Comparator"
date:   2021-05-17
last_modified_at: 2021-05-17
categories: [Algorithm]
tags: [Algorithm]
---

<br/>

문제 난이도 : Medium

<br/>

문제 유형 : Sorting

<br/>

문제 설명 간략 :  이름과 점수로 구성된 Player가 주어지고 점수 내림차순으로 정렬하고 점수가 같은 경우
사전순으로 정렬하는 Checker class를 선언한다.

<br/>

제약사항

- 0 <= score <= 1000
- 둘 이상의 플레이어들은 같은 이름을 갖을 수 있다.
- 플레이어 이름은 소문자 알파벳으로 주어진다.

<br/>

idea 

1. 숫자 먼저 비교, 같으면 문자 비교
   

<br/>

### 자바 풀이

```java
import java.util.*;

class Player {
    String name;
    int score;

    Player(String name, int score) {
        this.name = name;
        this.score = score;
    }
}

class Checker implements Comparator<Player> {
    // complete this method
    public int compare(Player a, Player b) {

        int result = -1;

        int aScore = a.score;
        String aName = a.name;

        int bScore = b.score;
        String bName = b.name;

        if(aScore < bScore) {
            result = 1;
        }else if(aScore == bScore) {
            int compare = aName.compareTo(bName);
            if(compare < 0) {
                result = -1;
            } else if(compare > 0) {
                result = 1;
            } else {
                result = 0;
            }
        }

        return result;
    }
}


public class Solution {

    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);
        int n = scan.nextInt();

        Player[] player = new Player[n];
        Checker checker = new Checker();

        for(int i = 0; i < n; i++){
            player[i] = new Player(scan.next(), scan.nextInt());
        }
        scan.close();

        Arrays.sort(player, checker);
        for(int i = 0; i < player.length; i++){
            System.out.printf("%s %s\n", player[i].name, player[i].score);
        }
    }
}

```

<br/>

출처

[해커랭크 문제](https://www.hackerrank.com/challenges/ctci-comparator-sorting/problem?h_l=interview&playlist_slugs%5B%5D=interview-preparation-kit&playlist_slugs%5B%5D=sorting)