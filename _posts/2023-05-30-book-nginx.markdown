---
layout: post
title:  "NGINX Cookbook 112가지 레시피로 배우는 고성능 부하분산, 보안, 서버 배포와 관리"
date:   2023-05-30
last_modified_at: 2023-05-30
categories: [nginx]
tags: [book]
---

책 리뷰 : 다양한 시나리오에 따른 설정 방법과 보안, 디버깅 트러블 슈팅에 관한 내용을 제공해준다.

<br/>

### 요청 빈도 제한

rate-limiting 모듈을 활용해 요청 빈도를 제한. 브루트포스 공격을 차단, 서버 리소스 고갈 문제 대응

<br/> 

### 캐시 성능

Cache-Control 헤더를 사용. (css, js 파일을 캐시)

<br/>

### 크로스 오리진, 리소스 공유

서비스 도메인이 아닌 다른 도메인을 통해 리소스를 제공할 때 브라우저가 원활히 접근하도록 CORS 정책 지정

<br/>

### HTTPS

모든 HTTP 트래픽을 HTTPS로 리다이렉트 방법.

<br/>

### HSTS

웹 브라우저가 HTTP로 요청을 보내지 않도록 강제

Strict-Transport-Security 헤더를 설정.

<br/>

출처 : OREILLY NGINX Cookbook 112가지 레시피로 배우는 고성능 부하분산, 보안, 서버 배포와 관리 옮김