---
layout: post
title:  "EFFECTIVE JAVA 모든 객체의 공통 메서드"
date:   2021-01-02
last_modified_at: 2021-01-02
categories: [JAVA]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item10 – equals는 일반 규약을 지켜 재정의하라.

equals 메서드의 동치 관계(equivalence relation)

|---|:---:|
|반사성(reflexivity)|* x is not null, x.equals(x) 는 true|
|대칭성(symmetry)|* x and y are not null, x.equals(y)가 true면 y.equals(x) true|
|추이성(transitivity)|* x, y and z are not null, x.equals(y)가 true이고, y.equals(z)이면 x.equals(z)는 true|
|일관성(consistency)|* x and y are not null, x.equals(y)를 반복해서 호출하면 항상 true를 반환하거나 항상 false를 반환|
|Null 이 아님|*x is not null, x.equals(null)은 false|

*#수학과 유사하다*.  
<br/>
Object의 equals는 거의 정확하다. 재정의하여 사용할 때는 다섯 가지 규약을 지켜야한다.  
<br/>

>Item11 – equals를 재정의하려 거든 hashCode도 재정의하라.  

hashCode 일반 규약  

- equals 비교에 사용되는 정보가 변경되지 않으면, 앱이 실행되는 동안 객체의 hashCode는 항상 같아야한다.
- equals가 두 객체를 같다고 판단하였으면, 두 객체의 hashCode는 같은 값을 반환해야한다.
- equals가 두 객체를 다르다고 판단했다면, 서로 다른 값을 반환할 필요는 없지만 다른 값을 반환해야 해시테이블의 성능이 좋아진다. ( 객체가 많아지면 해시테이블의 버킷 하나에 담겨 연결리스트처럼 동작하여 성능 저하 유발 O(n) ). 

<br/>
[Equals와 hashCode를 자동으로 만들어주는 구글 AutoValue 프레임워크](https://github.com/google/auto/blob/master/value/userguide/index.md) 

<br/>

>Item12 – toString을 항상 재정의하라.  

System.out.println으로 Object의 기본 toString 매서드를 찍었을 때 클래스_이름@16진수로_표시한_해시코드를 반환한다. 디버깅하기 쉽게 객체 정보를 명확히 담도록 재정의하자. (실제로는 디버깅 툴로 봤던 경우가 더 많았다… 자주 확인하고 보수해야하는 테스트 코드에서는 디버깅을 위해 재정의하는 편이 훨씬 나을 것 같다.)

<br/>

clone재정의와 Comparable은 코드를 보고 이해하는게 더 편하여 간략한 내용만 정리한다.  
clone은 생성자와 팩터리를 이용하는게 best.
comapareTo 메서드에서 필드 값을 비교할 때 정적 compare 메서드나 Comparator 인터페이스가 제공하는 비교 생성자를 사용하자.

<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>