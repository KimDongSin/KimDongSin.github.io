---
layout: post
title: React Context API란 무엇인가
description: Context API를 알아보자.
author: dongsin
date: 2024-05-24 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/jojeon4515/post/bd5f6da9-34ee-4f04-8afb-bb853341fb6f/image.png
---

## Context API란?
---
리액트의 Context API는 컴포넌트 트리 전체에 걸쳐서 전역적인 데이터를 공유할 수 있게 하는 기능이다.<br />
Context API를 사용하면 `props drilling`을 해결할 수 있다. <br />

`props drilling`=> 컴포넌트를 거쳐서 props를 전달하는 행위


## Context API 사용법
---
#### Context 생성
> `React.createContext`를 사용하여 conText를 생성한다.

#### Provider 컴포넌트
> `Context.Provider`를 사용하여 데이터를 하위 컴포넌트에 전달한다.

#### Consumer 혹은 useContext 훅
> `Context.consumer` 또는 `useContext`훅을 사용하여 하위 컴포넌트에서 데이터를 읽는다.



## 예시코드
---
테마 컨텍스트로 예시를 들어보자.

### 테마 컨텍스트 정의
---
먼저, 테마를 관리할 Context와 Provider를 정의한다.

```jsx
import React, { createContext, useState, useContext } from 'react';

// 테마 컨텍스트 생성
const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme((prevTheme) => (prevTheme === 'light' ? 'dark' : 'light'));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

// 커스텀 훅: 컨텍스트 사용을 쉽게 하기 위해
export function useTheme() {
  return useContext(ThemeContext);
}

```

### Provider 사용
---
`ThemeProvider`를 최상위 컴포넌트에서 사용하여 모든 하위 컴포넌트에 테마 정보를 제공한다.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import { ThemeProvider } from './ThemeContext';

ReactDOM.render(
  <ThemeProvider>
    <App />
  </ThemeProvider>,
  document.getElementById('root')
);
```

### 테마 정보를 읽어오는 컴포넌트
---
이제 `useTheme`훅을 사용하여 컴포넌트에서 테마 정보를 쉽게 사용할 수 있다.
```jsx
import React from 'react';
import { useTheme } from './ThemeContext';

function App() {
  const { theme, toggleTheme } = useTheme();

  return (
    <div className={theme === 'light' ? 'bg-white text-black' : 'bg-gray-800 text-white'} min-h-screen flex flex-col items-center justify-center>
      <h1 className="text-4xl mb-4">
        {theme === 'light' ? 'Light Theme' : 'Dark Theme'}
      </h1>
      <button 
        className="py-2 px-4 bg-blue-500 text-white rounded hover:bg-blue-700 transition"
        onClick={toggleTheme}
      >
        Toggle Theme
      </button>
    </div>
  );
}

export default App;

```

### 코드해석
---
#### Context 생성
* `ThemeContext`는 전역에서 테마 정보를 관리 할 수 있는 컨텍스트이다.
* `ThemeProvider`컴포넌트는 `theme`와 `toggleTheme`함수를 `value`로 전달하여 하위 컴포넌트에서 사용할 수 있게 한다.

#### Provider 사용
* `ThemeProvider`를 최상위 컴포넌트에서 감싸주어 하위 컴포넌트들이 테마 정보에 접근 할 수 있게 한다.

#### Consumer 사용
* `useTheme`커스텀 훅을 사용하여 `ThemeContext`의 값을 읽고, 테마 정보와 테마를 토글하는 함수를 제공한다.
* `App` 컴포넌트는 `theme` 값에 따라 배경과 텍스트 색상을 변경하고, 버튼을 클릭하면 테마를 변경할 수 있다.

<br />

### Context API의 단점
---
### 성능 문제
Context의 값이 변경되면 해당 Context를 구독하고 있는 모든 하위 컴포넌트가 리렌더링된다.<br />
이로 인해 불필요한 렌더링이 발생하여 `성능 저하`가 발생한다. <br />
<br />

### 상태관리의 복잡성
Context API는 간단한 상태 관리에는 적합하지만, 규모가 복잡해질 수록<br />
Context API만으로 상태를 관리하는 것은 복잡해 질 수 있다.<br />
따라서 전역상태관리 라이브러리를 사용하는 것이 옳다.

### 디버깅 어려움
Context API를 사용한 상태관리는 React DevTools에서 상태를 추적하기 어려울 수 있다.<br />
이는 상태의 변화가 어디서 발생했는지 파악하는 것을 어렵게 만들 수 있다.

## 결론
이와 같이 Context API를 사용하면 전역적으로 컴포넌트 트리 어디서든 쉽게 <br />
전역 상태관리가 가능해진다. 이를 통해 코드의 중복과 props drilling을 해결할 수 있다.<br />
<br />
Context API는 간단한 상태 관리에는 적합하지만 규모가 커짐에 따라서 전역상태관리 라이브러리를 사용하자.
