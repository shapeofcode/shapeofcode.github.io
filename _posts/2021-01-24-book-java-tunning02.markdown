---
layout: post
title:  "자바 성능 튜닝 이야기 - 3,4장 (String 관련, Collection 관련)"
date:   2021-01-24
last_modified_at: 2021-01-24
categories: [book, JAVA, TUNNING]
tags: [book, JAVA, TUNNING]
---

**String 관련**

-	스레드와 관련있으면 StringBuffer를 안전 여부와 상관이 없으면 StringBuilder를 사용한다.

<br/>

**Set 관련**

- HashSet , LinkedHashSet 성능 비슷 TreeSet 성능 차이 보임
- HashSet은 데이터 크기를 미리 알고 있을 때 미리 지정하면 성능상 유리
- TreeSet은 데이터를 순서에 따라 탐색하는 작업이 필요할 때 유의미

<br/>

**List 관련**
- ArrayList, Vector, LinkedList 데이터를 추가하는 시간은 비슷하다. 데이터를 가져오는 속도는 ArrayList > Vector > LinkedList 순으로 빠름. LinkedList는 특히 느리다. 그 이유는 Queue 인터페이스를 상속받았기 때문이다. Vector도 ArrayList 보다 훨씬 느린데 그 이유는 여러 스레드에서 접근할 경우를 방지하기 위해서 get() 메서드에 synchronized가 선언되어 있기 떄문이다. 삭제의 경우 마지막 값보다 첫번째 값을 삭제할 때 속도 차이가 난다. 그 이유는 0번 째를 삭제하면 나머지가 값의 위치를 변경해야 하기 때문이다.
Map 관련
- HashMap, Hashtable, TreeMap, LinkedHashMap 비슷하지만 트리 형태로 처리하는 TreeMap 클래스가 가장 느리다.

<br/>

애매할 때 쓰기 좋은 가장 일반적으로 사용되는 클래스

Set – HashSet

List – ArrayList

Map – HashMap

Queue - LinkedList

<br/>

출처 : 자바 성능 튜닝 이야기 이상민 지음

<br/>