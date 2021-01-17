---
layout: post
title:  "EFFECTIVE JAVA 제네릭"
date:   2021-01-04
last_modified_at: 2021-01-04
categories: [book, JAVA]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item26 – 로 타입은 사용하지 말라.

로 타입은 런 타임 시 예외를 발생 시킬 수 있다.

<br/>

>Item27 – 비검사 경고를 제거하라.  

코드를 작성하다 보면 익숙하게 보는 경고들이 있다. ClassCastException을 유발할 수 있는 요소를 제거하고 타입이 안전함을 주석으로 남기며 최대한 범위를 좁혀 @SuppressWarnings(“unchecked”)를 사용한다. 

<br/>

>Item28 - 배열보다는 리스트를 사용하라.  

배열 = 공변, 제네릭은 = 불공변. 배열은 런타임에는 타입 안전하지만 컴파일타임에는 그렇지 않다.

<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>