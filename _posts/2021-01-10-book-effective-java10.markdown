---
layout: post
title:  "EFFECTIVE JAVA 동시성"
date:   2021-01-10
last_modified_at: 2021-01-10
categories: [book]
tags: [book, EFFECTIVE JAVA 3/E]
---

>Item81 – wait와 notify보다는 동시성 유틸리티를 애용하라.

ConcurrentMap으로 구현한 동시성 정규화 맵

```java
public static String intern(String s) {
    String result = map.get(s);
    if (result == null) {
        result = map.putIfAbsent(s, s);
        if (result == null)
            result = s;
    }
    return result;
}
```
<br/>

출처 : EFFECTIVE JAVA 3/E 조슈아 블로크 지음

<br/>