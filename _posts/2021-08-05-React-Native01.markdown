---
layout: post
title:  "React Native - 소개"
date:   2021-08-05
last_modified_at: 2021-08-05
categories: [React Native]
tags: [React Native]
---

<br/>

1. 간단한 소개

React Native는 javascript를 이용하여 android,ios에서 모두 사용할 수 있는 native code를 작성할 수 있게 한다.

<br/>

React로 classes 또는 functinos components를 만들 수 있다. 

<br/>

- 핵심 컴포넌트

View는 UI를 만다는 기본이 되는 block이다. 
Android 개발자들은 Kotlin 또는 Java를 이용하여 개발하고 iOS 개발자들은 Swift 또는 Objective-C를 이용하는데 
React Native에서는 Javascript를 사용하여 React components 통해 view들을 부른다.

<br/>

![img.png](../assets/images/react-native01.png)

<br/>

React Native는 React components와 동일한 API구조를 사용한다.
	
2. 코어 컨셉

• Components
	
```javascript
import React, { Component } from 'react';
import { Text } from 'react-native';

class Cat extends Component {
  render() {
    return (
      <Text>Hello, I am your cat!</Text>
    );
  }
}
export default Cat;
```

React로부터 Component를 import하고 Cat class는 Compenet를 상속한다. 
Component class는 render() function이 있고 안에 무엇이있든 React element로 rendered된다. 
그리고 class compoenet로 export할 수 있다.

<br/>

• JSX

React와 React Native는 javavscript에 요소를 쓸 수 있게 JSX를 사용한다.

<br/>

• Custom Components

Core Components를 이용하여 Custom Compnents를 만들 수 있다.

```javascript
import React from 'react';
import { Text, TextInput, View } from 'react-native';

const Cat = () => {
  return (
    <View>
      <Text>Hello, I am...</Text>
      <TextInput
        style={{
          height: 40,
          borderColor: 'gray',
          borderWidth: 1
        }}
        defaultValue="Name me!"
      />
    </View>
  );
}
	
export default Cat;

import React from 'react';
import { Text, View } from 'react-native';

const Cat = () => {
  return (
    <View>
      <Text>I am also a cat!</Text>
    </View>
  );
}

const Cafe = () => {
  return (
    <View>
      <Text>Welcome!</Text>
      <Cat />
      <Cat />
      <Cat />
    </View>
  );
}

export default Cafe;
```

<br/>

Cafe는 부모 component이고 Cat은 자식 Component이다.

<br/>

• Props

Properties의 약자로 React components를 customize할 수 있게 해준다.

<br/>

```javascript
import React from 'react';
import { Text, View } from 'react-native';

const Cat = (props) => {
    return (
        <View>
        <Text>Hello, I am {props.name}!</Text>
        </View>
    );
}

const Cafe = () => {
    return (
        <View>
            <Cat name="Maru" />
            <Cat name="Jellylorum" />
            <Cat name="Spot" />
        </View>
    );
}

export default Cafe;
```

<br/>

• State

Component의 data storage 역활을 한다.

```javascript
import React, { Component } from "react";
import { Button, Text, View } from "react-native";

class Cat extends Component {
state = { isHungry: true };

    render() {
        return (
            <View>
                <Text>
                    I am {this.props.name}, and I am
                    {this.state.isHungry ? " hungry" : " full"}!
                </Text>
                    <Button
                        onPress={() => {
                            this.setState({ isHungry: false });
                        }}
                        disabled={!this.state.isHungry}
                        title={
                            this.state.isHungry ? "Pour me some milk, please!" : "Thank you!"
                        }
                    />
            </View>
        );
    }
}

class Cafe extends Component {
    render() {
        return (
            <>
                <Cat name="Munkustrap" />
                <Cat name="Spot" />
            </>
        );
    }
}

export default Cafe;
```

- State는 state object에 저장된다.
- This.setState의 key value로 값을 지정할 수 있다.

<br/>

출처

[https://reactnative.dev/docs/getting-started](https://reactnative.dev/docs/getting-started)
[https://reactnative.dev/docs/intro-react-native-components](https://reactnative.dev/docs/intro-react-native-components)
[https://reactnative.dev/docs/intro-react](https://reactnative.dev/docs/intro-react)