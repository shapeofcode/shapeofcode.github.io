---
layout: post
title:  "DO it! Vue.js 입문"
date:   2023-05-29
last_modified_at: 2023-05-29
categories: [Vue.js]
tags: [book]
---

### Vuejs 키워드

프론트엔드 프레임워크
- 상태관리
- 클라이언트 사이드 라우팅
- 컴포넌트 기반
- 명시적 렌더링(코어 라이브러리)


<br/> 

### 뷰 인스턴스
화면 개발을 위한 기본 단위, 돔 요소를 지정

뷰 인스턴스의 라이프 사이클 
<br/>
인스턴스 생성 -> beforeCreate -> created -> beforeMount -> mounted -> 인스턴스를 화면에 부착 -> beforeUpdate -> updated
-> 인스턴스 내용 갱신 -> beforeDestroy -> destroyed -> 인스턴스 소멸

### 뷰 컴포넌트
화면 구성 블록 (전역 / 지역) - 인스턴스에 등록

<br/>
컴포넌트 통신

상위 -> 하위 
v-bind, propsdata

<br/>

이벤트 발생
this.$emit, v-on, 이벤트 버스 방식

### 뷰 라우터
SPA에서 주로 사용
- 네스티드 라우터
- 네임드 뷰

<br/>

그외 기타 데이터 동기화나 웹팩 등 Vue에 관한 전반적으로 쉽고 빠르게 접근할 수 있는 책

<br/>

출처 : Do it! Vue.js 입문 장기효 지음

<br/>