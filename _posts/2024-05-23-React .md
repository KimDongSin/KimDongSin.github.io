---
layout: post
title: React custom hook
description: custom hook을 알아보자.
author: dongsin
date: 2024-05-23 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/jojeon4515/post/bd5f6da9-34ee-4f04-8afb-bb853341fb6f/image.png
---


## React 커스텀 훅 만드는 법
---
리액트 커스텀 훅을 만드는 방법은 재사용 가능한 로직을 함수로 추출하여 필요할 때 <br />
여러 컴포넌트에서 사용할 수 있도록 하는 것이다.

### 커스텀 훅 만드는 방법
---
1. 훅을 정의하는 함수 이름은 `use`로 시작한다. 
2. 리액트 훅을 사용하여 원하는 로직을 구현한다
3. 필요한 데이터를 반환하거나, 상태와 함수를 반환한다.


### 예제코드
---
## 윈도우 사이즈를 추적하는 커스텀 훅으로 예시를 살펴보자.

### 커스텀 훅 정의
```jsx
import { useState, useEffect } from 'react';

function useWindowSize() {
  // state를 사용하여 window의 width와 height를 저장.
  const [windowSize, setWindowSize] = useState({
    width: window.innerWidth,
    height: window.innerHeight,
  });

  useEffect(() => {
    // window resize 이벤트 핸들러
    function handleResize() {
      setWindowSize({
        width: window.innerWidth,
        height: window.innerHeight,
      });
    }

    // 이벤트 리스너를 추가.
    window.addEventListener('resize', handleResize);

    // 클린업 함수로 이벤트 리스너를 제거.
    return () => window.removeEventListener('resize', handleResize);
  }, []); // 빈 배열로 두어 컴포넌트가 마운트될 때 한 번만 실행되도록 함.

  return windowSize; // window의 크기를 반환.
}

```

### 컴포넌트에서 커스텀 훅 사용
```jsx
import React from 'react';
import useWindowSize from './useWindowSize'; // 커스텀 훅을 import

function MyComponent() {
  const { width, height } = useWindowSize(); // 커스텀 훅을 사용하여 window의 크기를 가져온다.

  return (
    <div>
      <h1>Window Size</h1>
      <p>Width: {width}px</p>
      <p>Height: {height}px</p>
    </div>
  );
}

export default MyComponent;

```

## 폼 입력 관리하는 커스텀 훅

### 커스텀 훅 정의
```jsx
import { useState } from 'react';

function useForm(initialValues) {
  const [values, setValues] = useState(initialValues);

  const handleChange = (event) => {
    const { name, value } = event.target;
    setValues({
      ...values,
      [name]: value,
    });
  };

  const resetForm = () => {
    setValues(initialValues);
  };

  return {
    values,
    handleChange,
    resetForm,
  };
}

```
---
### 컴포넌트에서 커스텀 훅 사용

```jsx
import React from 'react';
import useForm from './useForm'; // 커스텀 훅을 import.

function MyForm() {
  const { values, handleChange, resetForm } = useForm({ username: '', email: '' });

  const handleSubmit = (event) => {
    event.preventDefault();
    console.log('Form submitted:', values);
    resetForm(); // 폼을 초기화.
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>
          Username:
          <input
            type="text"
            name="username"
            value={values.username}
            onChange={handleChange}
          />
        </label>
      </div>
      <div>
        <label>
          Email:
          <input
            type="email"
            name="email"
            value={values.email}
            onChange={handleChange}
          />
        </label>
      </div>
      <button type="submit">Submit</button>
    </form>
  );
}

export default MyForm;

```


## 결론
---

커스텀 훅 이름은 `use`로 시작해야 한다. <br />
리액트 훅을 사용하여 재사용 가능한 로직을 커스텀 훅으로 추출한다.<br />
커스텀 훅은 필요한 데이터를 반환하거나, 상태와 함수를 반환할 수 있다. <br />

다양한 컴포넌트에서 커스텀 훅을 호출하여 동일한 로직을 재사용 할 수 있다.
