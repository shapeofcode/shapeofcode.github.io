---
layout: post
title:  "React Native - Linking Libraries"
date:   2021-08-10
last_modified_at: 2021-08-10
categories: [React Native]
tags: [React Native]
---

<br/>

Native dependencies를 추가해야하는 경우.

<br/>

1. native dependencies 설치

```shell
npm install <library-with-native-dependencies> --save
```

package.json 파일의 dependencies를 기준으로 libs를 링크한다.

<br/>

2. native dependencies link

```shell
npx react-native link
```

<br/>

출처

[https://reactnative.dev/docs/linking-libraries-ios](https://reactnative.dev/docs/linking-libraries-ios)