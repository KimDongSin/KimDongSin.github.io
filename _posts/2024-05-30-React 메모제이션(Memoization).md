---
layout: post
title: React 메모제이션(Memoization)이란?
description: 메모제이션(Memoization) 종류
author: dongsin
date: 2024-05-30 00:10 +09:00
categories: [React]
tags: [Redux, Redux ToolKit]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/jojeon4515/post/bd5f6da9-34ee-4f04-8afb-bb853341fb6f/image.png
---

## 메모제이션(Memoization)이란?
---
React의 메모제이션은 컴포넌트가 불필요한 리렌더링이 일어나지 않게 방지하여
<br />성능을 최적화하는 기술이다.<br />

이는 동일한 입력이 주어졌을 때, 컴포넌트가 이전에 계산된 결과를 재사용하는 것이다.<br />


## React 메모제이션의 종류
---
`React.memo`
`useMemo`
`useCallback`
이렇게 3가지가 존재한다.

## React.memo
---
`React.memo`는 고차 컴포넌트(HOC)로, 컴포넌트가 동일한 props로 리렌더링되는 것을 방지한다.<br />

### 예시코드
```jsx
import React from 'react';

const MyComponent = React.memo(({ name }) => {
  console.log('MyComponent 렌더링');
  return <div>{name}</div>;
});

export default MyComponent;
```
위 코드에서 `MyComponent`는 props가 변경되지 않으면 다시 렌더링되지 않는다. <br />

## useMemo
---
`useMemo`는 값이 변경될 때만 계산을 실행하고, 나머지 경우에는 이전에 계산된 값을 반환한다. <br />
이는 비용이 큰 계산을 메모제이션 하는 데 유용하다. <br />

```jsx
import React, { useState, useMemo } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState('');

  const expensiveCalculation = useMemo(() => {
    console.log('비싼 계산 실행');
    return count * 2;
  }, [count]);

  return (
    <div>
      <p>계산 결과: {expensiveCalculation}</p>
      <button onClick={() => setCount(count + 1)}>증가</button>
      <input value={text} onChange={(e) => setText(e.target.value)} />
    </div>
  );
}

export default MyComponent;
```
위 코드에서 `expensiveCalculation`은 `count`가 변경될 때만 다시 계산된다.

## useCallback
---

`useCallback`은 함수 메모이제이션하여 동일한 함수가 재생성되지 않도록 한다. <br />
이는 자식 컴포넌트에 콜백 함수를 전달할 때 유용하다.<br />

```jsx
import React, { useState, useCallback } from 'react';

const Button = React.memo(({ onClick }) => {
  console.log('Button 렌더링');
  return <button onClick={onClick}>클릭</button>;
});

function MyComponent() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState('');

  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>카운트: {count}</p>
      <Button onClick={handleClick} />
      <input value={text} onChange={(e) => setText(e.target.value)} />
    </div>
  );
}

export default MyComponent;
```

위 코드에서 `handleClick` 함수는 `count`가 변경될 때만 다시 생성된다.

## 결론
---
React 메모제이션은 성능 최적화를 위해 매우 유용하게 사용된다.<br />
메모제이션을 적절히 활용하여 불필요한 렌더링을 방지하고, 웹 성능을 향상시킬 수 있다. <br />

### 정리
1. `React.memo`: 컴포넌트가 동일한 props로 다시 렌더링되지 않도록 한다.
2. `useMemo`: 값이 변경될 때만 계산을 실행하고, 나머지 경우에는 이전에 계산된 값을 반환한다.
3. `useCallback`: 콜백함수를 메모이제이션하여 동일한 함수가 재생성되지 않도록 한다.


