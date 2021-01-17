---
layout: post
title:  "EFFECTIVE JAVA 일반적인 프로그래밍 원칙"
date:   2021-01-08
last_modified_at: 2021-01-08
categories: [book, JAVA]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item57 – 지역변수의 범위를 최소화하라.

가장 강력한 기법은 가장 처음 쓰일 때 선언하기 또한 모든 지역변수는 선언과 동시에 초기화해야 한다.

<br/>

>Item58 – 전통적인 for 문보다는 for-each문을 사용하라.  

성능 저하도 없고 버그도 예방해준다.

쓸 수 없는 세가지 상황

- 파괴적인 필터링 – 컬렉션을 순회하면서 선택된 원소를 제거해야 한다면 반복자의 remove 메서드를 호출해야 한다.
- 변형 – 리스트나 배열을 순회하면서 그 원소의 값 일부 혹은 전체를 교체해야 한다면 인덱스를 사용해야한다.
- 병렬 반복 – 여러 컬렉션을 병렬로 순회해야 한다면 각각의 반복자와 인덱스 변수를 사용해 엄격하고 명시적으로 제어해야 하다.

<br/>

>Item59 - 라이브러리를 익히고 사용하라.  

앞서 사용한 다른 프로그래머들의 경험을 활용한 단단한 코드 사용 가능. java.lang, java.util, java.io와 그 하위 패키지들에는 익숙해져야 한다.

<br/>

>Item60 - 정확한 답이 필요하다면 float와 double은 피하라.

금융 관련 계산과는 맞지 않다. 금융 계산에는 BigDecimal, int 혹은 long을 사용해야한다.
(개인적으로 금융권 프로그램에서는 주로 어떻게 쓰는지 궁금하다...)

<br/>

>Item61 - 박싱된 기본 타입보다는 기본 타입을 사용하라.

박싱된 기본 타입에 == 연산자를 사용하면 오류가 일어난다. 언박싱 과정에서 NullPointerException을 던질 수 있다.

<br/>

>Item63 - 문자열 연결은 느리지 주의하라.

문자열 연결 연산자로 문자열 n개를 잇는 시간은 n제곱에 비례한다. StringBuilder의 append를 사용하라.

<br/>

>Item64 - 객체는 인터페이스를 사용해 참조하라.

```java
클래스를 타입으로 사용
LinkedHashSet<Son> sonSet = new LinkedHashSet<>();

인터페이스를 타입으로 사용
Set<Son> sonSet = new LinkedHashSet<>();
```

<br/>

>Item66 – 네이티브 메서드는 신중히 사용하라.

저수준 자원이나 네이티브 라이브러리를 사용해야만 하는 상황을 제외하고는 지양한다.

<br/>

>Item67 – 최적화는 신중히 하라.

최적화 격언
- (맹목적인 어리석음을 포함해) 그 어떤 핑계보다 효율성이라는 이름 아래 행해진 컴퓨팅 죄악이 더 많다(심지어 효율을 높이지도 못하면서). – 윌리엄울프[Wulf72]
- (전체의 97% 정도인) 자그마한 효율성을 모두 잊자. 섣부른 최적화가 만악의 근원이다. – 도널드 크누스[Knuth74]
- 최적화를 할 때는 다음 두 규칙을 따르라.
  - 첫 번째, 하지마라.
  - 두 번째, (전문가 한정) 아직 하지 마라. 다시 말해, 완전히 명백하고 최적화되지 않은 해법을 찾을 때까지는 하지 마라. - M. A. 잭슨[Jackson75]

<br/>

>Item68 – 일반적으로 통용되는 명명 규칙을 따르라.

|식별자 타입  | 예 |
|---|:---:|
| 패키지와 모듈  | org.junit.jupiter.api, com.google.common.collect |
| 클래스와 인터페이스  | Stream, FutureTask, LinkedHashMap, HttpClient |
| 메서드와 필드  | remove, groupingBy, getCrc |
| 상수 필드  | MIN_VALUE, MEGATIVE_INFINITY|
| 타입 매개변수 | T, E, K, V, X, R, U, V, T1, T2 |

<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>