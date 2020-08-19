---
layout: post
title:  "[React] styled components 사용해보기"
categories : Coding!
tag :
- React
- CSS
- React-Native
date: 2020-04-22


---

리엑트에서 스타일을 정의하기는 매우 복잡했습니다. class를 만들어야하고 컴포넌트간 상속에 대해 많은 시간을 쏟아야 했습니다. 

하지만 **`styled components`를 사용하면 모든게 간편해집니다.** 심지어 React-Native에서도 CSS를 사용할 수 있습니다.

간단한 사용법을 알아보도록 하겠습니다.

<!-- more -->

# styled components

Docs : https://styled-components.com/docs/

#### 편리하게 CSS를!

1. ```bash
   $npm i --save styled-components
   ```

2.  사용하고자 하는데 import 합니다

   ```react
   import styled from 'styled-components';
   ```

#### 사용법

1. 스타일 정의하기

   ```react
   const 변수명 = styled.<html element>`
   ... CSS 넣기
   `
   ```

   형태로 작성합니다.

   - example

     ```react
     const Container = styled.div`
       height: 100vh;
       width: 100%;
       background-color: #bcc3c7;
     `;
     ```

2. 스타일 사용

   ```react
   class App extends Component {
     render() {
       return (
         <Container>
           <Button></Button>
           <Button></Button>
         </Container>
       );
     }
   }
   ```

   위에서 정의한 변수명을 태그처럼 사용해주기만 하면 됩니다.

3. props 전달

   props 를 전달하는 방법을 알아봅시다.

   - 스타일 정의하면서 props 넣어주기

     ```react
     background-color: ${(props) => (props.danger ? 'red' : 'green')};
     ```

   - 태그 지정하면서 props 보내주기

     ```react
     <Button danger></Button>
     ```

     danger props를 보내준 태그는 분홍색, 아닌 태그는 초록색을 보여줍니다.

전체 코드

```react
import React, { Component } from 'react';
import styled from 'styled-components';

class App extends Component {
  render() {
    return (
      <Container>
        <Button>Hello</Button>
        <Button danger>Hello</Button>
      </Container>
    );
  }
}
const Container = styled.div`
  height: 100vh;
  width: 100%;
  background-color: #bcc3c7;
`;

const Button = styled.button`
  border-radius: 50px;
  padding: 5px;
  min-width: 120px;
  color: white;
  font-weight: 600;
  -webkit-appearance: none;
  cursor: pointer;
  &:active,
  &:focus {
    outline: none;
  }
  background-color: ${(props) => (props.danger ? '#e74c3c' : '#2ecc71')};
`;

export default App;

```



#### React-Native에 사용하기

똑같이 import 하고 사용하면 됩니다.!

- ReactNative

  ```react
  import React from "react";
  import {StyleSheet, Text, View} from "react-native";
  import styled from "styled-components";
  
  const Container = styled.View`
  	flex:1;
  	justify-content: center;
  	...
  `
  
  const Title = styled.Text`
  	font-weight: 600;
  	font-size: 32px
  `
  
  export default class App extends React.Component {
      render() {
  	return (
      	<Container>
          	<title>Good!</title>
          </Container>
      )
      }
  }
  
  
  ```











