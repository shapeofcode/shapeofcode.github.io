---
layout: post
title:  "EFFECTIVE JAVA 직렬화"
date:   2021-01-11
last_modified_at: 2021-01-11
categories: [JAVA]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item87 – 커스텀 직렬화 형태를 고려해보라.

객체의 물리적 표현과 논리적 표현의 차이가 클 때 기본 직렬화 형태를 사용하면 문제가 생긴다.
- 공개 API가 현재의 내부 표현 방식에 영구히 묶인다.
- 너무 많은 공간을 차지할 수 있다.
- 시간이 너무 많이 걸릴 수 있다.
- 스택 오버플로를 일으킬 수 있다.

어떤 직렬화 형태를 택하든 직렬화 가능 클래스 모두에 직렬 버전 UID를 명시적으로 부여하자.
```java
private static final long serialVersionUID = <무작위 long 값>;
```
<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>