---
layout: post
title:  "EFFECTIVE JAVA 람다와 스트림"
date:   2021-01-06
last_modified_at: 2021-01-06
categories: [book]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item42 – 익명 클래스보다는 람다를 사용하라.

타입을 명시해야 코드가 더 명확할 때만 제외하고는, 람다의 모든 매개변수 타입은 생략하자, 이유는 컴파일러가 타입 정보 대부분을 제네릭에서 얻기 때문이다.

<br/>

>Item43 – 람다보다는 메서드 참조를 사용하라.  

|메소드 참조 유형 | 예 | 같은 기능을 하는 람다 |
|---|:---:|---|
| 정적 | Integer::parseInt | str -> Integer.parseInt(str) |
| 한정적(인스턴스) | Instant.now()::isAfter | Instant then = Instant.now(); <br/> t -> then.isAfter(t) |
| 비한정적(인스턴스) | String::toLowerCase | str -> str.toLowerCase() |
| 클래스생성자 | TreeMap<K,V>::new | () -> new TreeMap<K,V>() |
| 배열생성자 | int[]::new | len ->new int[len] |

<br/>

>Item45 - 스트림은 주의해서 사용하라.  

스트림에 맞는 상황

- 원소들의 시퀀스를 일관되게 변환한다.
- 원소들의 시퀀스를 필터링한다.
- 원소들의 시퀀스를 하나의 연산을 사용해 결합한다.(더하기, 연결하기, 최솟값 구하기 등)
- 원소들의 시퀀스를 컬렉션에 모은다.(공통된 속성을 기준으로 묶어가며)
- 원소들의 시퀀스에서 특정 조건을 만족하는 원소를 찾는다.

<br/>

>Item48 - 스트림 병렬화는 주의해서 적용하라

스트림의 소스가 ArrayList, HashMap, HashSet, ConcurrentHashMap의 인스턴스거나 배열, int 범위, long 범위일 때 병렬화의 효과가 가장 좋다. 

<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>