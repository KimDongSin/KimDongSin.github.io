---
layout: post
title: React useId hook
description: React useId hook을 알아보자.
author: dongsin
date: 2024-05-31 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/jojeon4515/post/bd5f6da9-34ee-4f04-8afb-bb853341fb6f/image.png
---

## React useId란?
`useId`는 React 18에서 도입된 새로운 hook으로, 고유한 식별자를 생성하기 위해 사용된다. <br />
특히 SSR(Server-Side Rendering) 환경에서 유용하며, 클라이언트와 서버가 동일한 ID를 갖도록 <br />
보장해준다. 주로 접근성 관련 속성이나 리스트의 키를 생성할 때 유용하다.<br />

## 언제 사용하는가?
* 서버 사이드 렌더링(SSR) 환경
    * 서버와 클라이언트가 동일한 ID를 갖도록 보장하여, 클라이언트에서의 초기렌더링과 서버에서의
    * 렌더링이 일치하게 한다. 
* 리스트의 키(key)
    * 컴포넌트의 고유한 식별자를 생성하여, React가 컴포넌트를 효율적으로 업데이트 할 수 있게 한다.
* 접근성 관련 속성
    * 폼 요소의 `id`와 `htmlFor` 속성 등에 사용하여, 접근성을 향상시킨다.
    

## 예시코드

```jsx
import React, { useId } from 'react';

function MyComponent() {
  const id = useId();

  return (
    <div>
      <label htmlFor={id}>Name:</label>
      <input id={id} type="text" />
    </div>
  );
}

export default MyComponent;
```
위 코드에서 `useId`는 고유한 `id`를 생성하여, `labal`과 `input`이 동일한 ID를 공유하도록 한다.

### 리스트의 키로 사용하기
```jsx
import React, { useId } from 'react';

function ItemList({ items }) {
  return (
    <ul>
      {items.map(item => {
        const id = useId();
        return <li key={id}>{item}</li>;
      })}
    </ul>
  );
}

export default ItemList;

```
위 코드에서 `useId`는 각 리스트 항목에 고유한 키를 제공하여, React가 리스트를<br />
효율적으로 업데이트 할 수 있도록 한다.<br />


## 결론 
---
`useId`는 React 18에서 도입된 유용한 Hook으로, SSR환경에서 곻유한 ID를 보장하고,<br />
리스트의 키 및 접근성 관련 속성을 생성하는 데 도움을 준다. <br />
이를 통해 React 애플리케이션의 성능과 접근성을 향상 시킬 수 있다. <br />




