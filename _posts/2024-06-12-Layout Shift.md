---
layout: post
title: Layout Shift에 대해
description: Layout Shift 발생 원인과 해결법
author: dongsin
date: 2024-06-12 00:10 +09:00
categories: [React]
tags: [React, Layout Shift]
pin: false
math: true
mermaid: true
image:
  path:  https://www.oncrawl.com/wp-content/uploads/2020/09/What-is-Cumulative-Layout-Shift-250px.png
---

## Layout Shift란?
---
렌더링 중인 웹 페이지에서 요소들이 예상치 않게 움직이는 현상을 의미한다.<br />
사용자가 페이지를 로드하는 동안에도 발생할 수 있으며, 이는 사용자 경험에 부정적인 영향을 미칠 수 있다. <br />

## Layout Shift 발생 원인
---
### 요소 렌더링 지연
이미지나 스크립트 로딩 지연으로 인해 발생할 수 있다.

### 동적 콘텐츠 추가
JS를 통해 동적으로 콘텐츠를 추가할 때, 초기 렌더링 시에 위치를 예측할 수 없어 발생할 수 있다.

### 폰트 로딩
폰트가 로드될 때까지 기본 폰트가 사용되다가 폰트가 변경되면서 발생할 수 있다.


## 예시코드
---
Layout Shift가 발생하는 상황을 예시코드로 살펴보자.
```jsx
import React, { useState, useEffect } from 'react';

const App = () => {
  const [width, setWidth] = useState('100px');

  useEffect(() => {
    setTimeout(() => {
      setWidth('200px'); // 2초 후에 너비를 변경하여 Layout Shift 발생
    }, 2000);
  }, []);

  return (
    <div className="box" style={{ width: width, height: '100px', backgroundColor: 'lightblue', margin: '10px' }}>
      Box
    </div>
  );
}

export default App;
```

## Layout Shift 해결 방법
---
### 이미지 크기 지정
이미지의 크기를 사전에 정의하여 공간을 확보한다.

### CSS 애니메이션 사용
CSS 트랜지션 또는 애니메이션을 활용하여 요소의 크기나 위치 변경 시 부드럽게 처리한다.

### 레이아웃 사이즈 계산
요소가 동적으로 추가될 때, 사전에 레이아웃 사이즈를 계산하여 예상치 않은 이동을 방지한다.

## 결론
---
Layout Shift는 사용자 경험에 부정적인 영향을 미칠 수 있는 문제이다. <br />
위 방법들을 활용하여 Layout Shift를 최소화하고, 사용자가 예상치 못한 레이아웃 변화를<br />
경험하는 불편함을 최소화한다.<br />
<br />
React에서도 성능 최적화와 UX 개선을 위해 Layout Shift를 주의 깊게 관리하고<br />
사용자가 페이지를 부드럽게 경험할 수 있도록 하자.<br />