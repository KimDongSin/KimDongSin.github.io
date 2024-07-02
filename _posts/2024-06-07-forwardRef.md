---
layout: post
title: React forwardRef
description: React forwardRef 개념정리
author: dongsin
date: 2024-06-07 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path:  https://velog.velcdn.com/images/jojeon4515/post/bd5f6da9-34ee-4f04-8afb-bb853341fb6f/image.png
---

## React forwardRef 개념
---
`forwardRef`는 React에서 고차 컴포넌트를 만들 때 사용되는 함수이다. <br />
**이 함수는 컴포넌트에 전달된 ref를 다른 컴포넌트로 전달할 수 있게 해준다.** <br />
이를 통해 부모 컴포넌트가 자식 컴포넌트의 DOM 노드나 React 인스턴스에 접근할 수 있게 된다.<br />

## 예시코드
---
예시 코드는 `forwardRef`를 사용하여 부모 컴포넌트가 자식 컴포넌트의 DOM노드에 접근하는 방법이다.
```jsx
import React, { useRef, forwardRef } from 'react';

// 자식 컴포넌트
const FancyInput = forwardRef((props, ref) => (
  <input ref={ref} className="fancy-input" />
));

// 부모 컴포넌트
const ParentComponent = () => {
  const inputRef = useRef(null);

  const focusInput = () => {
    // inputRef.current는 자식 컴포넌트의 DOM 노드를 가리킨다.
    inputRef.current.focus();
  };

  return (
    <div>
      <FancyInput ref={inputRef} />
      <button onClick={focusInput}>Focus the input</button>
    </div>
  );
};

export default ParentComponent;
```

## 결론
---

`forwardRef`는 부모 컴포넌트가 자식 컴포넌트의 DOM 노드 또는 클래스 인스턴스에 접근할 수 있게 하는 유용한 기능이다. 
