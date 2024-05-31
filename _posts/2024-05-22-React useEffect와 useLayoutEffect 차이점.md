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
> 컴포넌트의 생애 주기 또는 데이터의 생애 주기에 따라 특정 코드를 실행시키고 싶을 때 사용하는 훅

useEffect는 생애주기도 고려하지만 의존성 배열에 따른 데이터변화도 고려한다.
의존성 배열이 바뀔 때마다 `useEffect`훅을 다시 실행한다.

API로 데이터를 가져온다고 가정하면 일단 DOM을 한번 그리고 그 다음에 
데이터를 받아오고 다시 한번 더 그린다.

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

마찬가지로 API로 데이터를 가져온다고 가정하면
화면을 그리기전에 데이터를 받아와서 한번에 화면에 그리게 된다.

하지만 데이터를 로딩이 너무 오래걸리면 화면에 아무것도 그려지지 않을 수도 있다.


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
