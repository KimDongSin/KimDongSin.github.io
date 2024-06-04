---
layout: post
title: Zustand 사용법
description: Zustand를 알아보자.
author: dongsin
date: 2024-06-04 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://github.com/pmndrs/zustand/raw/main/bear.jpg
---

## Zustand란?
---
Zustand는 React에서 전역상태 관리를 위한 라이브러리이다. <br />
간단하고 최소한의 API로 전역 상태를 관리할 수 있게 해준다. <br />

현재 Redux보다 더 간단하게 사용할 수 있는 상태 관리 솔루션을 찾는 개발자들에게 인기가 많은 편이다.

## 개념정리
* Store
    * Zustand에서 상태는 store에 저장된다. 
    * store는 하나의 객체로 구성되며, 상태 값과 이를 변경하는 함수들을 포함한다.
* Selector
    * store에서 특정 상태 값만을 선택하여 사용하는 방법이다.
* Middleware
    * 상태 업데이트 전후에 추가적인 동작을 정의할 수 있는 기능이다.

## 예시코드
---

### 설치
```bash
npm install zustand
```

### 상태 관리 스토어 생성
```js
// store.js
import create from 'zustand';

// 상태 관리 스토어 생성
const useStore = create((set) => ({
  count: 0, // 초기 상태 값
  increment: () => set((state) => ({ count: state.count + 1 })), // 상태 업데이트 함수
  decrement: () => set((state) => ({ count: state.count - 1 }))
}));

export default useStore;

```

### 컴포넌트에서 상태 사용
```js
// App.js
import React from 'react';
import useStore from './store';

function App() {
  const { count, increment, decrement } = useStore();

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
    </div>
  );
}

export default App;
```

위의 코드에서 `useStore`는 상태 값(count)과 상태를 변경하는 함수(`increment`, `decrement`)를 <br />
제공하는 훅이다. `useStore` 훅을 사용하여 상태를 읽고 업데이트 할 수 있다.

## 결론
---
Zustand는 간단하고 효율적인 상태관리 라이브러리로, 최소한의 설정으로 전역상태를 관리 할 수 있다.<br />
Redux보다 러닝커브가 낮고 보다 간편하고, 효율적으로 사용할 수 있어서 인기가 많다.


[Zustand 공식문서](https://docs.pmnd.rs/zustand/getting-started/introduction)