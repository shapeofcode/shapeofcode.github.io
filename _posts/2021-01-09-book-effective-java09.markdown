---
layout: post
title:  "EFFECTIVE JAVA 예외"
date:   2021-01-09
last_modified_at: 2021-01-09
categories: [JAVA]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item69 – 예외는 진짜 예외 상황에만 사용하라.

제어 흐름에 사용하지 마라.

<br/>

>Item72 – 표준 예외를 사용하라.  

널리 재사용되는 예외들

| 예외 | 주요 쓰임 |
|---|:---:|
| IllegalArgumentException | 허용하지않는 값이 인수로 건네졌을 때(null은 따로 NullPointerException으로 처리) |
| IllegalStateException | 객체가 메서드를 수행하기에 적절하지 않은 상태일 때 |
| NullPointerException | null을 허용하지 않는 메서드에 null을 건넸을 때 |
| IndexOutOfBoundsException | 인덱스가 범위를 넘어섰을 때 |
| ConcurrentModificationException | 허용하지 않는 동시 수정이 발견됐을 때 |
| UnsupportedOperationException | 호출한 메서드를 지원하지 않을 때 |

<br/>

>Item73 - 추상화 수준에 맞는 예외를 던지라.  

예외 번역을 통해 상위 계층에 어울리는 고수준 예외를 던지면서 근본 원인도 알려주어 오류를 분석하기에 좋다.

<br/>

>Item74 - 메서드가 던지는 모든 예외를 문서화하라.

@throws 태그로 문서화하되, 비검사 예외는 메서드 선언의 throws 목록에 넣지 말자. 

<br/>

>Item75 - 예외의 상세 메시지에 실패 관련 정보를 담으라.

실패 순간을 포착하려면 발생한 예외에 관여된 모든 매개변수와 필드의 값을 실패 메시지에 담아야 한다. 

<br/>

>Item77 - 예외를 무시하지 말라.

빈 catch블록을 무시하고 넘어가면 문제가 생길 수 있다.

<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>