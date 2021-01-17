---
layout: post
title:  "EFFECTIVE JAVA 메서드"
date:   2021-01-07
last_modified_at: 2021-01-07
categories: [book, JAVA]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item49 – 매개변수가 유효한지 검사하라.

JAVA7에 추가된 java.util.Objects.requireNonNull 메서드는 null 검사에 유용하다.
```java
this.strategy = Objects.requireNonNull(strategy,”전략”);
```
매개 변수들의 제약들은 문서화하고 코드 시작 부분에서 명시적으로 검사해야한다.

<br/>

>Item50 – 적시에 방어적 복사본을 만들라.  

클래스가 클라이언트로부터 받은 혹은 클라이언트로 반환하는 구성요소가 가변이라면 반드시 방어적으로 복사해야한다.
Date 대신 Instant를 사용한다. (LocalDateTime이나 ZonedDateTime 도 가능)

<br/>

>Item51 – 메서드 시그니처를 신중히 설계하라.  

- 메서드 이름을 신중히 짓자
- 편의 메서드를 너무 많이 만들지 말자
- 매개변수 목록을 짧게 유지하자 (4개 이하) – 같은 타입의 매개변수가 여러 개 연달아 나오는 경우는 지양
- 매개변수의 타입으로는 클래스보다는 인터페이스가 더 낫다.
- boolean보다는 원소 2개짜리 열거 타입이 낫다. (가독성, 확장성)

```java
Thermometer.newInstance(true)
Thermometer.newInstance(TemperatureScale.CELSIUS)
```

<br/>

>Item53 - 가변인수는 신중히 사용하라.

필수 매개변수는 가변인수앞에 두고, 성능 문제까지 고려하자.

<br/>

>Item54 - null이 아닌, 빈 컬렉션이나 배열을 반환하라.

null을 반환하는 API는 사용하기 어렵고 오류 처리 코드도 늘어난다.

<br/>

>Item56 - 공개된 API 요소에는 항상 문서화 주석을 작성하라.

API를 올바로 문서화하려면 공개된 모든 클래스, 인터페이스, 메서드, 필드 선언에 문서화 주석을 달아야 한다. 메서드용 문서화 주석에는 클라이언트가 해당 메서드를 호출하기 위한 전제조건을 모두 나열하고 사후 조건도 모두 나열해야한다.

```java
/**
*이 리스트에서 지정한 위치의 원소를 반환한다.
*
* <p>이 메서드는 상수 시간에 수행됨을 보장하지 <i>않는다</i>.구현에 따라 원소의 위치에 
* 비례해 시간이 걸릴 수 도 있다.
*
* @param index 반환할 원소의 인덱스; 0 이상이고 리스트 크기보다 작아야 한다.
* @return 이 리스트에서 지정한 위치의 원소
* @throws IndexOutofBoundsException index가 범위를 벗어나면,
*		즉, ({@code index < 0 || index >= this.size()})이면 발생한다.
*/
E get(int index);
``` 

<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>