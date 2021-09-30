---
layout: post
title:  "React Native - Troubleshooting"
date:   2021-08-07
last_modified_at: 2021-08-07
categories: [React Native]
tags: [React Native]
---

<br/>

#### Port already in use

Metro bundler는 8081 port에서 구동된다. Port 8081에서 구동중인 프로세스를 죽이는 방법

<br/>

Linux

```shell
sudo lsof -i :8081
kill -9 <PID>
```

Port parameter를 이용하여 다른 port를 사용할 수 있다.

```shell
npx react-native start --port=8088
```

<br/>

#### NPM locking error

npm WARN locking Error: EACCES를 마주하면 다음을 실행하라

```shell
sudo chown -R $USER ~/.npm
sudo chown -R $USER /usr/local/lib/node_modules
```

<br/>

#### Missing libraries for React

수동으로 React Native를 추가할때 관련 dependencies들이 모두 추가되었는지 확인해야한다.

Likning Libraries 참조.

CocoaPods를 사용한다면 Podfile에 subspecs를 등록했는지 확인해야한다.

```text
pod 'React', :path => '../node_modules/react-native', :subspecs => [
    'RCTText',
    'RCTImage',
    'RCTNetwork',
    'RCTWebSocket',
]
```

<br/>

그 다음 pod install를 실행하고 Pods 디렉토리가 만들어졌는지 확인해야한다. 
CocoaPods가 .xcworkpsace를 생성하여 관련 dependencies드를 사용할 수 있게 알려줄 것이다.

<br/>

#### No transports available

React Native는 WebSockets를 위해 polyfill을 사용한다. 
Import React from 'react'에 포함되는데 다른 WebSockets를 써야하는 경우(ex Firebase) react-native 뒤에 넣어라.

<br/>

```javascript
import React from 'react';
import Firebase from 'firebase';
```

<br/>

#### Shell Command Unresponsive Exception

```shell
Execution failed for task ':app:installDebug'.
com.android.builder.testing.api.DeviceException: com.android.ddmlib.ShellCommandUnresponsiveException
```

<br/>

이런 에러가 보이면 android/build.gradle에 있는 Gradle 버전을 1.2.3으로 낮추어라.

<br/>

#### react-native init hangs

Npx react-native init에 문제가 있으면 verbose mode로 실행하여라.

```shell
npx react-native init --verbose
```

<br/>

#### Unable to start react-native package manager (on Linux)

##### Case 1: Error "code":"ENOSPC","errno":"ENOSPC"

Linux에서 watchman이 inotify 폴더 개수를 모니터링하는 부분에서 생기는 문제이다. 다음 명령어를 실행하라.


```shell
echo fs.inotify.max_user_watches=582222 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

<br/>

출처

[https://reactnative.dev/docs/troubleshooting](https://reactnative.dev/docs/troubleshooting)