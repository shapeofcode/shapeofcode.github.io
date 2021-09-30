---
layout: post
title:  "React Native - Platform Specific Code"
date:   2021-08-08
last_modified_at: 2021-08-08
categories: [React Native]
tags: [React Native]
---

<br/>

React Native는 어떤 platform에서 app이 구동되는지 탐지할 수 있는 module을 제공한다.

```javascript
import { Platform, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  height: Platform.OS === 'ios' ? 200 : 100
});
```

Platform.select method는 'ios' | 'android' | 'native' | 'default' key를 제공한다.

<br/>

```javascript
import { Platform, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    ...Platform.select({
      ios: {
        backgroundColor: 'red'
      },
      android: {
        backgroundColor: 'green'
      },
      default: {
        // other platforms, web for example
        backgroundColor: 'blue'
      }
    })
  }
});
```

<br/>

platform의 특정 components도 반환할 수 있다.

```javascript
const Component = Platform.select({
  ios: () => require('ComponentIOS'),
  android: () => require('ComponentAndroid')
})();

<Component />;

const Component = Platform.select({
    native: () => require('ComponentForNative'),
    default: () => require('ComponentForWeb')
})();

<Component />;    
```

<br/>

#### Android Version 탐지

```javascript
import { Platform } from 'react-native';

if (Platform.Version === 25) {
  console.log('Running on Nougat!');
}
```

버전은 Android API version을 의미한다.

<br/>

#### iOS Version 탐지

```javascript
import { Platform } from 'react-native';

const majorVersionIOS = parseInt(Platform.Version, 10);
if (majorVersionIOS <= 9) {
  console.log('Work around a change in behavior');
}
```

<br/>

#### 특정 Platform 확장자

project에 다음과 같이 파일을 만들면 component를 인식 할 수 있다.

```text
BigButton.ios.js
BigButton.android.js
```

```javascript
import BigButton from './BigButton';
```

<br/>

#### NodeJS/Web과 공유할 경우

Android/iOS에 차이가 없다면 React Native와 ReactJS간에 교환할 수 있다.

```text
Container.js # picked up by Webpack, Rollup or any other Web bundler
Container.native.js # picked up by the React Native bundler for both Android and iOS (Metro)
```

```javascript
import Container from './Container';
```

<br/>

출처

[해커랭크 문제](https://leetcode.com/explore/learn/card/queue-stack/239/conclusion/1393/)