---
layout: post
title:  "React Native - Text Input, ScrollView, List Views"
date:   2021-08-05
last_modified_at: 2021-08-05
categories: [React Native]
tags: [React Native]
---

<br/>

1.TextInput

Text를 입력하는곳 onChangeText를 통해 text가 변경될 때마다 호출한다.

<br/>

```javascript
import React, { useState } from 'react';
import { Text, TextInput, View } from 'react-native';

const PizzaTranslator = () => {
    const [text, setText] = useState('');
    return (
        <View style={{padding: 10}}>
            <TextInput
                style={{height: 40}}
                placeholder="Type here to translate!"
                onChangeText={text => setText(text)}
                defaultValue={text}
            />
            <Text style={{padding: 10, fontSize: 42}}>
                {text.split(' ').map((word) => word && '🍕').join(' ')}
            </Text>
        </View>
    );
}

export default PizzaTranslator;

```

<br/>

2. ScrollView

여러 개 components와 views를 담을 수 있다.

```javascript
import React from 'react';
import { Image, ScrollView, Text } from 'react-native';

const logo = {
    uri: 'https://reactnative.dev/img/tiny_logo.png',
    width: 64,
    height: 64
};

const App = () => (
<ScrollView>
    <Text style={{ fontSize: 96 }}>Scroll me plz</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{ fontSize: 96 }}>If you like</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{ fontSize: 96 }}>Scrolling down</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{ fontSize: 96 }}>What's the best</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{ fontSize: 96 }}>Framework around?</Text>
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Image source={logo} />
    <Text style={{ fontSize: 80 }}>React Native</Text>
</ScrollView>
);

export default App;
```

<br/>

3. List Views

<br/>

3-1. FlatList. 화면에 보여지는것만 render한다.

<br/>

FlatList  component는 두개의 속성을 갖는다. Data와 renderItem. Data는 list의
Data를 의미하고 renderItem은 source로부터 하나의 아이템을 가져와 formatted된 component를 render할 수 있게 return시킨다.

<br/>

3-2 SectionList. iOS의 UITableView와 유사하며 data set을 logical sections으로 구분하고 싶다면 headers 이용하여 render한다.

<br/>

출처

[https://reactnative.dev/docs/handling-text-input](https://reactnative.dev/docs/handling-text-input)