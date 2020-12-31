---
layout: post
title:  "EFFECTIVE JAVA 객체 생성과 파괴"
date:   2021-01-01
last_modified_at: 2021-01-01
categories: [book]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item1 – 생성자대신 팩터리 메서드를 고려하라.

```java
Date now = Date.from(instant);
Set<Asset> portFolio = EnumSet.of(STOCK,GOLD,COIN);
BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
```
위 함수를 보면 그동안 from , of , valueOf 메소드를 아무렇지 않게 사용하고 있었다. 하지만 메소드를 쓰는데 너무 자연스러운 이유는 잘 지어진 이름으로 인한 반한 될 객체의 특성을 잘 알 수 있기 때문이다. 불필요한 객체 생성을 할 필요도 없어진다.  
<br/>

알아두면 좋은 정적 팩터리 메서드 명명 방식  

|---|:---:|
|from|하나의 매개 변수를 받아서 해당 타입의 인스턴스를 형 변환하여 반환할 때|
|of  | 여러 개의 매개변수를 받아 적합한타입의 인스턴스를 반환할 때|
|valueOf | from 과 of의 자세한 버전|
|instance or getInstance | 같은 인스턴스라는 것을 보장하지 않으면서 인스턴스 반환할 때|
|create or newInstsance | 새로운 인스턴스를 생성해 반환을 보장할 때|
|getType | 다른 클래스에 팩터리 메서드를 정의할 때|
|newType | 다른 클래스에 팩터리 메서드를 정의할 때|
|type | getType과 newType의 간결한 버전|

<br/>

>Item2 – 생성자에 매개변수가 많다면 빌더를 고려하라.  

점층적 생성자 패턴, 흔히 매개변수가 늘어날 경우 많이 사용한다.  
자바빈즈 패턴, 이 또한 많이 사용하는 패턴으로 메서드 호출을 여러 번 해야하는 단점이 있다.  
빌더 패턴, 최근에는 자바 라이브러리를 사용하면서 많이 접하는 패턴이다. 메소드 채이닝이라고도 하며 매개변수가 4개 이상 많아질 경우 큰 장점이 있다. 간결하고 안전한 특징이있다. 

<br/>

>Item7 – 다 쓴 객체 참조를 해제하라.  

메모리를 직접 관리하는 클래스는 메모리 누수에 주의해야함을 이야기하고 있다. Java는 GC를 갖추고 있어서 메모리 관리에 신경 쓰지 않는 경우가 많은데 메모리를 다루는 자바 코드는 null 처리와 같은 참조 해제를 행해 주어야 한다. 캐시,리스너,콜백 또한 마찬가지이다.

<br/>

>Item9 – try-finally 보다는 try-with-resources를 사용하라. 

BufferedReader, InputStream, OutpuStream 자원을 항상 닫아주는 코드로 finally 이후에 써주는 걸로 익숙하다. 여러 개가 쓰일 경우 코드가 지저분해지며 오류 사항에 대하여 놓치는 부분이 생길 수 있다.  

[try-with-resources 오라클 문서](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html) 

<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>