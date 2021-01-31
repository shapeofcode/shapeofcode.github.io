---
layout: post
title:  "자바 성능 튜닝 이야기 - 23장 (튜닝 절차 관련)"
date:   2021-01-28
last_modified_at: 2021-01-28
categories: [book, JAVA, TUNNING]
tags: [book, JAVA, TUNNING]
---

**기초 법칙 – 암달의 법칙**
성능 개선율 = 1 / (1-P) + P/S
P 성능 개선 가능한 부분의 비율 S 개선된 정도
ex) 성능 개선 가능한 부분이 100% P = 1, 2배의 성능 향상이 이루어 졌다면 S = 2 성능 개선율 2

<br/>

**성능 튜닝 절차**
1. 원인 파악
2. 목표 설정
3. 튜닝 실시
4. 개선율 확인
5. 결과 정리 및 반영

<br/>

**성능 튜닝 비법**
- 하나만 보지 말아라 (서버장비, OS, Application, Webserver, Network, Client)
- 큰 놈을 없애라
- 깊게 알아야 한다.
- 결과 공유는 선택이 아닌 필수!

<br/>

출처 : 자바 성능 튜닝 이야기 이상민 지음

<br/>