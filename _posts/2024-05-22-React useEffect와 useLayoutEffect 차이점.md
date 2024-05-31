---
layout: post
title: React useEffect와 useLayoutEffect 차이점
description: useEffect와 useLayoutEffect를 알아보자.
author: dongsin
date: 2024-05-22 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/jojeon4515/post/bd5f6da9-34ee-4f04-8afb-bb853341fb6f/image.png
---

## useEffect와 useLayoutEffect의 차이점
> 두 훅의 차이는 언제 실행되는지에 차이점이 존재한다.


## useEffect란?
`useEffect`는 컴포넌트가 화면에 `그려진 후` 실행된다. <br />
주로 서버에서 데이터를 가져오는 작업(API), 구독 설정, 타이머설정(`setTimeout, setInterval`)

```jsx
import React, { useState, useEffect } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // 컴포넌트가 화면에 그려진 후 실행됨
    document.title = `You clicked ${count} times`;

    // 정리 함수: 컴포넌트가 사라질 때 실행됨
    return () => {
      console.log('Cleanup');
    };
  }, [count]); // count가 바뀔 때마다 실행됨

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

```

## useLayoutEffect란?
`useLayoutEffect`는 컴포넌트가 `화면에 그려지기 전에` 실행된다.<br />

화면이 그려지기 전에 해야할 작업들을 수행한다. <br />
>예를 들면 레이아웃이나 스타일 조정 등등 

```jsx
import React, { useState, useLayoutEffect, useRef } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);
  const divRef = useRef(null);

  useLayoutEffect(() => {
    // 컴포넌트가 화면에 그려지기 전에 실행됨
    if (divRef.current) {
      divRef.current.style.color = 'red';
    }
  }, [count]); // count가 바뀔 때마다 실행됨

  return (
    <div ref={divRef}>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}

```

<br />

## 결론

### 실행되는 시점
`useEffect`는 컴포넌트가 화면에 그리고 난 후 실행된다. <br />
`useLayoutEffect`는 컴포넌트가 화면에 그려지기 전에 실행된다.<br />

### 언제 사용하는가?
### `useEffect` <br />
데이터를 가져오거나, 구독 설정, 타이머설정 등 대부분의 경우는 useEffect가 적합하다. <br />
<br />

### `useLayoutEffect`
**화면이 그려지기 전에 DOM을 조작해야 하는 경우에 사용한다.**
