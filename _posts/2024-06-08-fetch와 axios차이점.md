---
layout: post
title: fetch와 axios차이점
description: fetch와 axios차이점 기록
author: dongsin
date: 2024-06-05 00:10 +09:00
categories: [JavaScript]
tags: [JavaScript, API 통신]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/rnrn99/post/22df0c8a-be0a-4d65-a0f8-5d9eb14e841d/image.png
---

## fetch API란?
---
`fetch` API는 네트워크 요청을 보내기 위해 JS에서 기본적으로 제공하는 기능이다. <br />
Promise를 사용하여 비동기적으로 작업을 처리하며, JSON을 포함한 다양한 형식의 데이터를 처리할 수 있다.<br />

```jsx
// GET 요청 예시
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => {
    if (!response.ok) {
      throw new Error('네트워크 응답이 성공적이지 않다');
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('에러 발생:', error));

// POST 요청 예시
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'foo',
    body: 'bar',
    userId: 1
  })
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('에러 발생:', error));

```

## axios 라이브러리
---
`axios`는 Promise기반의 HTTP 클라이언트로, 브라우저와 Node.js에서 모두 작동한다. <br />
`fetch`에 비해 사용하기 더 간편하며, 인터셉터, 자동 JSON변환, 취소 토큰,<br />
타임아웃 설정 등의 추가 기능을 제공한다.

```jsx
import axios from 'axios';

// GET 요청 예시
axios.get('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => console.log(response.data))
  .catch(error => console.error('에러 발생:', error));

// POST 요청 예시
axios.post('https://jsonplaceholder.typicode.com/posts', {
  title: 'foo',
  body: 'bar',
  userId: 1
})
  .then(response => console.log(response.data))
  .catch(error => console.error('에러 발생:', error));
```

## fetch와 axios의 차이점
---

* 호환성 및 지원
    * `fetch`는 최신 브라우저에서 기본적으로 제공되지만, 구형 브라우저에서는 풀리필이 필요하다.
    * `axios`는 브라우저와 Node.js에서 모두 사용할 수 있으며, 보다 광범위한 호환성을 제공한다.
---
* API의 간편성
    * `fetch`는 기본적인 기능을 제공하지만, 예외 처리가 상대적으로 복잡하다. <br />
     상태 코드를 수동으로 확인하고 에러를 처리한다.
    * `axios`는 더 간단한 API를 제공하며, 응답 데이터를 자동으로 JSON으로 변환해 주고, <br />
    인터셉터를 통해 요청 및 응답을 중간에 가로챌 수 있다.
---
* 기능성
    * `fetch`는 요청 취소 기능을 기본적으로 제공하지 않지만, `AbortController`를 통해 구현할 수 있다.
    * `axios`는 요청 취소, 타임아웃 설정, 요청 및 응답 인터셉터 등 다양한 추가 기능을 기본적으로 제공한다.
---

## 결론
---
`fetch`와 `axios`는 각기 다른 장단점을 가지고 있어 상황에 따라 적절하게 사용할 수 있다.<br />
간단한 요청이나 최신 브라우저 환경에서는 `fetch`가 유용할 수 있으며 보다 복잡한 기능이 필요하거나
Node.js환경에서도 사용할 경우 `axios`가 더 적합하다.