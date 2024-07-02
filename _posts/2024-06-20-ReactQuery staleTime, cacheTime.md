---
layout: post
title: staleTime과 cacheTime
description: staleTime과 cacheTime 개념정리
author: dongsin
date: 2024-06-19 00:10 +09:00
categories: [ReactQuery]
tags: [React, ReactQuery]
pin: false
math: true
mermaid: true
image:
  path:  https://t1.kakaocdn.net/kakao_tech/image/2022/06/images/01.png
---

## staleTime이란?
---
`staleTime`은 쿼리 데이터가 "stale"(낡은) 상태가 되기 전까지의 시간을 나타낸다. <br />
이 기간 동안 React Query는 데이터를 신선한 것으로 간주하고, 쿼리가 다시 활성화되더라도 <br />
네트워크 요청을 하지 않는다. 기본 값은 `0`이며, 이는 쿼리 데이터가 즉시 stale 상태가 됨을 의미한다. <br />

* 즉시 stale 상태: `staleTime: 0` (기본값)
* 데이터가 5분 동안 신선한 상태로 유지: `staleTime: 300000` (밀리초 단위)

## cacheTime이란?
---
`cacheTime`은 데이터가 "stale"상태가 된 후, 데이터와 캐시에 남아 있는 시간을 나타낸다. 
<br />기본 값은 `5분`이다. 

이 시간이 지나면 데이터는 메모리에서 제거되며, 쿼리가 다시 활성화되면 새 네트워크 요청이 발생한다. <br />

* 기본 값: `cacheTime: 300000` (5분)
* 캐시를 1시간 동안 유지: `cacheTime: 3600000` (밀리초 단위)

## 예시코드
---

React Query를 사용하여 `staleTime`과 `cacheTime`을 설정하는 방법을 살펴보자.

```jsx
import React from 'react';
import { useQuery, QueryClient, QueryClientProvider } from 'react-query';
import axios from 'axios';

// QueryClient 생성
const queryClient = new QueryClient();

const fetchTodos = async () => {
  const { data } = await axios.get('https://jsonplaceholder.typicode.com/todos');
  return data;
};

const Todos = () => {
  const { data, isLoading, isError } = useQuery(
    'todos', 
    fetchTodos, 
    {
      staleTime: 5000, // 5초 동안 데이터가 신선한 상태로 유지됨
      cacheTime: 10000 // 10초 동안 캐시된 데이터가 메모리에 유지됨
    }
  );

  if (isLoading) {
    return <div>Loading...</div>;
  }

  if (isError) {
    return <div>Error fetching data</div>;
  }

  return (
    <div>
      <h3>Todo List</h3>
      <ul>
        {data.map(todo => (
          <li key={todo.id}>{todo.title}</li>
        ))}
      </ul>
    </div>
  );
};

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Todos />
    </QueryClientProvider>
  );
}

export default App;
```

### 코드분석
---
#### QueryClient 생성
`QueryClient`를 생성하고 `QueryClientProvider`를 사용하여 React 컴포넌트 트리에 주입시킨다.

#### fetchTodos 함수
axios를 사용하여 API로부터 데이터를 가져오는 함수이다.

#### useQuery 훅
* `todos`라는 키를 사용하여 `fetchTodos` 함수를 호출하여 데이터를 가져온다.
* `staleTime`을 `5000` (5초)로 설정하여 데이터를 5초 동안 신선하게 유지한다.
* `cacheTime`을 `10000` (10초)로 설정하여 데이터를 10초 동안 메모리에 캐싱한다.

#### 조건부 렌더링
데이터가 로딩 중일 때, 오류가 발생했을 때, 그리고 성공적으로 데이터를 가져왔을 때 <br />
각각 다른 내용을 렌더링한다. <br />

## 결론
---
`staleTime과 `cacheTime`을 사용하여 데이터가 얼마나 오래 신선하게 유지되고,<br />
캐시에 얼마나 오래 남아있을 지를 제어할 수 있다. 이를 통해 불필요한 네트워크 요청을 줄이고<br />
애플리케이션의 성능을 최적화 시킬 수 있다.<br />