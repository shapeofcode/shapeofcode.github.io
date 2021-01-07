---
layout: post
title:  "EFFECTIVE JAVA 열거타입과 애너테이션"
date:   2021-01-05
last_modified_at: 2021-01-05
categories: [book]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item34 – int 상수 대신 열거 타입을 사용하라.

필요한 원소를 컴파일 타임에 알 수 있는 상수 집합이라면 열거타입을 사용해야한다. (가독성, 타입 안전성)

<br/>

>Item36 – 비트 필드 대신 EnumSet을 사용하라.  

EnumSet 내부는 비트 백터로 구성되어있고 비트 필드 수준의 명료함과 성능을 제공한다. 

<br/>

>Item39 - 명명 패턴보다 애너테이션을 사용하라.  

명명패턴의 단점

- 오타로 인한 점검 누락
- 올바른 프로그램 요소에 사용된다는 보장을 해주지 못함
- 프로그램 요소를 매개변수로 전달할 방법이 없다 

<br/>

>Item40 - @Override 애너테이션을 일관되게 사용하라

예를 들어 equals를 재정의하려고 그대로 함수명을 사용하게 되면 overloading이 된다.

재정의법
```java
@Override public Boolean equals(Bigram b) {
	return b.first == first && b.second == second;
}
```

<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>