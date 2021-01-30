---
layout: post
title:  "자바 성능 튜닝 이야기 - 5,6장 (반복문 관련, static 관련)"
date:   2021-01-25
last_modified_at: 2021-01-25
categories: [book, JAVA, TUNNING]
tags: [book, JAVA, TUNNING]
---

**반복문 관련**

- switch는 숫자 비교 시 if보다 가독성이 좋다. 오라클에서 권장
- JDK7부터 switch case는 String을 비교할 수 있는데 각 값들을 hashCode로 변환하고, 그 값이 작은 것부터 정렬한 다음에 String의 equals() 메서드를 사용하여 실제 값과 동일한지 비교한다. 숫자가 정렬되어있기 때문에 작은 숫자부터 큰 숫자를 비교하는게 가장 빠르고 case가 많아지면 소요되는 시간이 오래 걸린다.
- while문보다 for문을 권장.(무한 루프에 빠질 수 있기 때문이다.)
- 
```java
int listSize = list.size();
for(int loop =0; loop < listSize; loop++)
```

size() 메서드 반복 호출이 없어지므로 더 빠르게 처리된다.

<br/>

**static 관련**
- 설정 파일 정보는 static으로 관리하는게 좋음 (매번 로딩하면 성능 저하)
- static은 반드시 메모리에 올라가며 GC 대상이 되지 않는다.
- 객체를 다시 생성한다고 해도 그 값은 초기화되지 않고 해당 클래스를 사용하는 모든 객체에서 공유

<br/>

출처 : 자바 성능 튜닝 이야기 이상민 지음

<br/>