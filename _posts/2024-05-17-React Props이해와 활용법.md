---
layout: post
title: React Props이해와 활용법
description: React Props를 알아보자.
author: dongsin
date: 2024-05-17 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/jojeon4515/post/bd5f6da9-34ee-4f04-8afb-bb853341fb6f/image.png
---



## React Props이해와 활용법
---
React는 컴포넌트 기반의 라이브러리로, 재사용 가능한 UI컴포넌트를 만드는 데 중점을 둔다. <br />
이러한 컴포넌트 간의 데이터 전달을 위해 `props`가 중요한 역할을 한다.<br />

## React Props란 무엇인가?
---
`props`는 부모 컴포넌트가 자식 컴포넌트에게 값을 전달하기 위해 사용하는 객체이다. <br />
이는 컴포넌트 간의 데이터 흐름을 단방향으로 유지하며, 컴포넌트 간의 결합도를 낮춰 재사용성을 높이는 중요한 개념이다. <br />


### 예시코드

```jsx
function Greeting(props){
    return <h1>Hello, {props.name}</h1>
}

function App() {
    return <Greeting name="Kim" />;
}
```

예시코드에서 `Greeting`컴포넌트는 `name`이라는 prop을 받아와서 이를 사용하여 h1태그의 인사말을 출력한다.<br />
`App`컴포넌트는 `Greeting`컴포넌트에 `name` prop을 전달한다.<br />


<br />

## Props의 특징
---
### **읽기 전용** <br />
props는 부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달하는 역할을 하며, <br />
**자식 컴포넌트 내에서는 props을 변경할 수 없다.** 이는 컴포넌트의 상태와 데이터를<br />
예측가능하게 유지하는 데 도움을 준다.


### **단방향 데이터 흐름**<br />
데이터는 항상 부모에서 자식으로 흐른다. 이는 데이터의 흐름을 명확히 이해하고 디버깅을 용이하게 한다.<br />

<br />


## Props와 State의 차이
---
### props
부모 컴포넌트가 자식 컴포넌트에 전달하는 데이터, 읽기 전용이며 자식 컴포넌트에서 변경할 수 없다.

### State
컴포넌트 내에서 관리되는 데이터. 컴포넌트가 스스로 관리하며 변경할 수 있다.
<br />

## Prop Drilling과 Context API
---
프로젝트가 커지면 여러 단계에 걸쳐 props를 전달해야 하는 경우가 발생한다.<br />
이를 `prop drilling`이라고 하며, 코드 가독성을 떨어뜨릴 수 있다. 이를 해결하기 위해<br />
React에서는 Context API를 제공하여 컴포넌트 트리 전체에 걸쳐 데이터를 공유할 수 있다. <br />

```jsx
import React, { createContext, useContext } from 'react';

// 1. Context 생성
const UserContext = createContext();

function UserProvider({ children }) {
  const user = { name: 'John Doe', email: 'john.doe@example.com' };

  return (
    <UserContext.Provider value={user}>
      {children}
    </UserContext.Provider>
  );
}

function UserProfile() {
  // 2. Context 사용
  const user = useContext(UserContext);
  return <div>{user.name} - {user.email}</div>;
}

function App() {
  return (
    <UserProvider>
      <UserProfile />
    </UserProvider>
  );
}

export default App;
```

`userProvider` 컴포넌트는 `UserContext.Provider`를 사용하여 자식 컴포넌트에게 사용자 정보를 내려준다.<br />
`UserProfile` 컴포넌트는 `useContext`훅을 사용하여 `UserContext`로 부터 사용자 정보를 받아온다.<br />

<br />

## 결론
---
React에서 props는 컴포넌트 간의 데이터 전달을 위한 도구이다. <br />
props를 잘 활용하면 컴포넌트의 재사용성과 유지보수성을 편하게 만들 수 있다. <br />

### 핵심정리

* **props**는 부모 컴포넌트가 자식 컴포넌트에게 데이터를 전달하는 객체
* **읽기 전용**이며, 데이터 흐름은 *단방향**이다.
* **Props로 함수 전달**을 통해 자식 컴포넌트가 부모 컴포넌트의 함수를 호출할 수 있다.
* **Props와 State**의 차이점을 이해하고, 상황에 맞게 사용해야 한다.
* **Prop Drilling** 문제를 해결하기 위해 **Context API**를 사용할 수 있다.
