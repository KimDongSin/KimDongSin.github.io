---
layout: post
title: Styled Components란
description: Styled Components를 알아보자.
author: dongsin
date: 2024-05-27 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://miro.medium.com/v2/resize:fit:1200/1*iqdJuZ4kY9P3GlX9BYfGGA.png
---

## Styled Components란?
**Styled Components**는 CSS-in-JS 라이브러리로, React 컴포넌트안에서 스타일을 작성할 수 있게 해준다.<br />
또한 스타일링을 컴포넌트화하여 재사용성과 유지보수성을 높여준다.<br />

## 설치
```
npm install styled-components 또는, yarn add styled-components
```

## 기본 사용법

```jsx
import React from 'react';
import styled from 'styled-components';

// 스타일드 컴포넌트 정의
const Button = styled.button`
  background: ${props => props.primary ? 'blue' : 'gray'};
  color: white;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

// 컴포넌트 사용
function App() {
  return (
    <div>
      <Button primary>Primary Button</Button>
      <Button>Secondary Button</Button>
    </div>
  );
}

export default App;

```

스타일 컴포넌트를 정의하는 위치 또한 갈린다.

> 코드 윗줄에 쓰는 스타일, 코드 맨 아랫줄에 쓰는 스타일 혹은 파일로 나눠서 관리하는 스타일이 존재한다.

### Props를 활용한 스타일링
---
styled-components는 props를 사용하여 동적으로 스타일링이 가능하다.

```jsx
import React from 'react';
import styled from 'styled-components';

// 스타일드 컴포넌트 정의
const Container = styled.div`
  padding: 2em;
  background: papayawhip;
`;

const Button = styled.button`
  background: ${props => props.primary ? 'blue' : 'gray'};
  color: white;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;

  &:hover {
    background: ${props => props.primary ? 'darkblue' : 'darkgray'};
  }
`;

// 컴포넌트 사용
function App() {
  return (
    <Container>
      <Button primary>Primary Button</Button>
      <Button>Secondary Button</Button>
    </Container>
  );
}

export default App;

```

### 글로벌 스타일
또한, `reset.css`와 같은 글로벌 스타일도 적용할 수 있다.

```jsx
import React from 'react';
import styled, { createGlobalStyle } from 'styled-components';

// 글로벌 스타일 정의
const GlobalStyle = createGlobalStyle`
  body {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
  }
`;

// 스타일드 컴포넌트 정의
const Container = styled.div`
  padding: 2em;
  background: papayawhip;
`;

const Button = styled.button`
  background: ${props => props.primary ? 'blue' : 'gray'};
  color: white;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;

  &:hover {
    background: ${props => props.primary ? 'darkblue' : 'darkgray'};
  }
`;

// 컴포넌트 사용
function App() {
  return (
    <>
      <GlobalStyle />
      <Container>
        <Button primary>Primary Button</Button>
        <Button>Secondary Button</Button>
      </Container>
    </>
  );
}

export default App;

```

## 결론
---
style-components는 컴포넌트 기반 스타일링이 가능하여 각 컴포넌트가 자신의 스타일을 가질 수 있어서<br />
재사용성과 유지보수성이 높아진다. <br />

또한 props으로 동적 스타일링도 가능하고, `createGlobalStyle`을 사용하여 전역 스타일을 쉽게 적용할 수 있다. <br />

