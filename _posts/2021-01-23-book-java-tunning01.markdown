---
layout: post
title:  "자바 성능 튜닝 이야기 - 내가 만든 프로그램의 속도를 알고 싶다"
date:   2021-01-23
last_modified_at: 2021-01-23
categories: [book, JAVA, TUNNING]
tags: [book, JAVA, TUNNING]
---

**절대 사용하면 안되는 메서드**

- static void gc() – GC 수행
- static void exit(int satus) – 자바 VM중지
- static void runFinalization() – 호출 하면 참조 해제 작업을 기다리는 모든 객체의 finalize() 메서드를 수동으로 수행해야 한다.

<br/>

**System.nanoTime 이 System.currentTimeMillis() 보다 빠르다. JDK5.0 이상 사용**

<br/>

**JMH 사용해볼것!**
```java
@BenchmarkMode({ Mode.AverageTime}) … 평균 응답 시간 측정
@OutputTimeUnit(TimeUnit.MILLISECONDS) … 출력 시간 단위
public class CompareTimeJMH {

	@GenerateMicroBenchmark … 측정 대상이 되는 메서드를 선언
	public Dummy Data makeObject() {
		HashMap<String, String> map = new HashMap<String, String>(1000000);
		ArrayList<String> list = new ArrayList<String>(1000000);
		return new DummyData(map, list);
	}
}
```


<br/>

출처 : 자바 성능 튜닝 이야기 이상민 지음

<br/>