---
layout: post
title: ReactQuery와 useQuery
description: ReactQuery와 useQuery개념정리.
author: dongsin
date: 2024-06-15 00:10 +09:00
categories: [ReactQuery]
tags: [React, ReactQuery]
pin: false
math: true
mermaid: true
image:
  path:  https://t1.kakaocdn.net/kakao_tech/image/2022/06/images/01.png
---

## React Query란?
---
리액트 쿼리는 서버에서 데이터를 가져와 리액트 컴포넌트에서 쉽게 사용할 수 있도록 해주는 라이브러리이다. <br />
데이터를 캐싱하고 관리하는 기능을 제공하여, 최적화된 데이터를 구축할 수 있다. <br />

## React Query특징
---
#### 캐싱 및 상태관리
자동으로 데이터를 캐싱하여 중복 요청을 방지하고, 서버 상태관리를 용이하게 해준다.

#### 쉬운 데이터 동기화
서버와의 데이터 동기화를 자동화하여 UI 업데이트를 실시간으로 반영할 수 있다. 

#### 네트워크 요청 관리
데이터 fetching을 간편하게 관리하고, 인터셉터와 재시도 로직을 통해 네트워크 오류에 대응할 수 있다.

---
**포스팅이 너무 길어질 것 같아서 나눠서 포스팅하도록 하겠다.**
먼저 `useQuery`에 대해서 알아보겠다. 

## useQuery 예시코드
---
```jsx
import React from 'react';
import { useQuery } from 'react-query';

const fetchPosts = async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  if (!response.ok) {
    throw new Error('네트워크 오류 - 데이터를 가져올 수 없습니다.');
  }
  return response.json();
};

const Posts = () => {
  const { data, isLoading, isError } = useQuery('posts', fetchPosts);

  if (isLoading) return <p>Loading...</p>;
  if (isError) return <p>Error fetching data...</p>;

  return (
    <div>
      <h2>Posts</h2>
      <ul>
        {data.map(post => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default Posts;
```

#### queryKey
useQuery 훅에서는 데이터를 캐싱하고 관리하기 위해 사용하는 고유 식별자이다.<br />
일반적으로 문자열 배열로 구성되며, 쿼리의 종류나 매개변수를 지정하는 데 사용된다. <br />

#### queryFn
데이터를 가져오는 함수로, useQuery에 전달된다. 이 함수는 실제 데이터 fetching을 담당하며,<br />
비동기 작업을 수행하여 데이터를 반환한다.


## 결론
---
리액트 쿼리는 데이터 fetching과 관리를 위한 강력한 도구로, 쉽게 캐시 관리와 UI업데이트를 처리 할 수 있다. <br />
이를 통해 더 좋은 사용자 경험을 제공할 수 있게 된다. <br />

[공식문서](https://tanstack.com/query/latest/docs/framework/react/overview)