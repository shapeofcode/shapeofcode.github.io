---
layout: post
title:  "React Native - JSX"
date:   2021-08-05
last_modified_at: 2021-08-05
categories: [React Native]
tags: [React Native]
---

<br/>

JSX는 React.createElement(component, props, ...children)의 syntax이다. 

```javascript
<MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>
```

compiles into 

```javascript
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Click Me'
)
```

<br/>

```javascript
<div className="sidebar" />
```

compiles into 

```javascript
React.createElement(
  'div',
  {className: 'sidebar'}
)
```

<br/>

### React Element 타입 지정


<br/>

#### React는 Scope 안에 있어야 한다.

JSX가 React.createElemnt로 compile 된 이후, React library는 JSX code scope에 있어야한다.

```javascript
import React from 'react';
import CustomButton from './CustomButton';

function WarningButton() {
  // return React.createElement(CustomButton, {color: 'red'}, null);
  return <CustomButton color="red" />;
}
```

Javascript bundler를 사용하지 않고 <script> tag에서 React를 불러왔으면 React global로 scope이 잡힌다.

<br/>

#### dot notation

React Component 구성요소를 JSX에서 dot-notation으로 참조할 수 있다.

```javascript
import React from 'react';

const MyComponents = {
  DatePicker: function DatePicker(props) {
    return <div>Imagine a {props.color} datepicker here.</div>;
  }
}

function BlueDatePicker() {
  return <MyComponents.DatePicker color="blue" />;
}
```

<br/>

#### 사용자 정의 components는 대문자로 해야한다.

```javascript
import React from 'react';

// Correct! This is a component and should be capitalized:
function Hello(props) {
  // Correct! This use of <div> is legitimate because div is a valid HTML tag:
  return <div>Hello {props.toWhat}</div>;
}

function HelloWorld() {
  // Correct! React knows <Hello /> is a component because it's capitalized.
  return <Hello toWhat="World" />;
}
```

<br/>

#### 실행 중에 타입 선택

```javascript
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
  photo: PhotoStory,
  video: VideoStory
};

function Story(props) {
  // 올바른 사용법입니다! 대문자로 시작하는 변수는 JSX 타입으로 사용할 수 있습니다.
  const SpecificStory = components[props.storyType];
  return <SpecificStory story={props.story} />;
}
```

<br/>

### JSX안에서 prop 사용

#### JavaScript 표현을 Props로 

javascript 표현을 {} 안에 넣어서 JSX안에서 prop으로 사용

```javascript
<MyComponent foo={1 + 2 + 3 + 4} />
```

<br/>

if, for는 Javascript 표현식이 아니기 때문에 JSX 밖의 주변코드로 사용할 수 있다.

```javascript
function NumberDescriber(props) {
  let description;
  if (props.number % 2 == 0) {
    description = <strong>even</strong>;
  } else {
    description = <i>odd</i>;
  }
  return <div>{props.number} is an {description} number</div>;
}
```

#### 문자열 리터럴


같은 표현

```javascript
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

문자열 리터럴으 넘겨줄 때 HTML 이스케이프 처리가 되지 않는다.

같은 표현

```javascript
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />
```

<br/>

Propes 기본값은 "True"

```javascript
<MyTextBox autocomplete />

<MyTextBox autocomplete={true} />
```

<br/>

props에 해당하는 객체를 이미 가지고 있다면, ...를 연산자로 사용해 전체 객체를 그대로 넘겨줄 수 있다.

```javascript
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

<br/>

### JSX에서 자식 다루기

<br/>

#### 문자열 리터럴

props.children은 그 문자열이 됩니다.

```javascript
<MyComponent>Hello world!</MyComponent>
```

props.children은 "Hello world" 이다.

HTML은 이스케이프 처리가 되지 않으며, 일반적으로 HTML을 쓰는 방식으로 JSX를 쓸 수 있다.

```html
<div>This is valid HTML &amp; JSX at the same time.</div>
```

<br/>

처음과 끝 공백제거, 빈줄 제거 태그에 붙어있는 개행 제거, 문자열 중간에 있는 개행은 한개의 공백으로 대체.

```html
<div>Hello World</div>

<div>
  Hello World
</div>

<div>
  Hello
  World
</div>

<div>

  Hello World
</div>
```

위 내용은 전부 똑같이 렌더링 된다.

<br/>

#### JSX를 자식으로 사용하기

<br/>

중첩된 컴포넌트를 보여줄 때 유용

```javascript
<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
```

<br/>

React component는 element로 이루어진 배열을 반환할 수 있다.

```javascript
render() {
  // 리스트 아이템들을 추가적인 엘리먼트로 둘러쌀 필요 없습니다!
  return [
    // key 지정을 잊지 마세요 :)
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}
```

<br/>

#### JavaScript 표현식을 자식으로 사용하기

{}에 감싸서 JavaScript 표현식도 자식으로 넘길 수 있다.

```javascript
<MyComponent>foo</MyComponent>

<MyComponent>{'foo'}</MyComponent>
```

<br/>

```javascript
function Item(props) {
  return <li>{props.message}</li>;
}

function TodoList() {
  const todos = ['finish doc', 'submit pr', 'nag dan to review'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
    </ul>
  );
}
```

<br/>

```javascript
function Hello(props) {
  return <div>Hello {props.addressee}!</div>;
}
```

JavaScript 표현식은 다른 타입의 자식과 같이 쓸 수 있다.

<br/>

#### 함수를 자식으로 사용하기

props.children은 다른 prop들과 마찬가지로 어떤 형태의 데이터도 넘겨질 수 있다.

```javascript
// 자식 콜백인 numTimes를 호출하여 반복되는 컴포넌트를 생성합니다.
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>This is item {index} in the list</div>}
    </Repeat>
  );
}
```

#### boolean, null, undefined는 무시된다.

렌더링 되지 않는다. 아래 내용은 모두 동일하게 렌더링.

```javascript
<div />

<div></div>

<div>{false}</div>

<div>{null}</div>

<div>{undefined}</div>

<div>{true}</div>
```

<br/>

React element들을 조건부 렌더링할 때 유용

```javascript
<div>
  {showHeader && <Header />}
  <Content />
</div>
```

<br/>

0과 같은 falsy 값들은 React가 렌더링 한다. 아래 내용의 props.message가 빈 배열일 때 0d을 출력한다. 

```javascript
<div>
  {props.messages.length &&
    <MessageList messages={props.messages} />
  }
</div>
```

<br/>

&& 앞의 표현식이 진리값이 되도록 바꾸면 된다.

```javascript
<div>
  {props.messages.length > 0 &&
    <MessageList messages={props.messages} />
  }
</div>
```

<br/>

false, true, null 또는 undefined와 같은 값들을 출력하고 싶다면 문자열로 전환해야 한다.

```javascript
<div>
  My JavaScript variable is {String(myVariable)}.
</div>
```

<br/>

출처

[https://reactjs.org/docs/jsx-in-depth.html](https://reactjs.org/docs/jsx-in-depth.html)