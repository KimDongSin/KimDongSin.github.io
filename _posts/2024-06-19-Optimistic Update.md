---
layout: post
title: Optimistic Update란
description: Optimistic에 대해 알아보자.
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

## Optimistic Update 개념
`Optimistic Update`는 사용자 경험을 향상시키기 위해 UI에서 데이터 변경을 즉시 반영하는 기술이다.<br />

#### 이 기능을 React Query에서는 두 가지 방법으로 제공한다 <br />
1. UI를 통한 방식
2. 캐시를 직접 조작하는 방식.

각 방식은 서로 다른 상황에서 유용하게 적용될 수 있다.

### 주요특징
---
* 사용자 인터페이스에서 즉시 데이터 업데이트
* 비동기 서버 응답을 기다리는 동안 사용자 경험 개선

## UI를 통한 Optimistic Update
---
UI를 통한 Optimistic Update는 가장 간단한 형태로, 직접적으로 상호작용하지 않는다. <br />
예를 들어 TodoList에 새로운 항목을 추가할 때 다음과 같은 코드를 사용할 수 있다. <br />

### 예시코드
---
```jsx
import React from 'react';
import { useMutation, useQueryClient } from 'react-query';

const Todos = () => {
  const queryClient = useQueryClient();

  const addTodoMutation = useMutation({
    mutationFn: (newTodo: string) => axios.post('/api/todos', { text: newTodo }),
    onSettled: async () => {
      await queryClient.invalidateQueries({ queryKey: ['todos'] });
    },
  });

  const { isPending, variables, mutate, isError } = addTodoMutation;

  const handleAddTodo = async (newTodo: string) => {
    mutate(newTodo);
  };

  return (
    <div>
      <ul>
        {todoQuery.items.map((todo) => (
          <li key={todo.id}>{todo.text}</li>
        ))}
        {isPending && <li style={{ opacity: 0.5 }}>{variables}</li>}
      </ul>
      {isError && (
        <li style={{ color: 'red' }}>
          {variables}
          <button onClick={() => mutate(variables)}>Retry</button>
        </li>
      )}
    </div>
  );
};

```

이 코드에서 `addTodoMutation`을 통해 새로운 Todo를 추가할 때, `isPending` 상태에 따라 임시 항목을 UI에 추가한다.<br />

이 항목은 Optimistic Update로, 서버 응답을 기다리지 않고 즉시 UI에 반영된다. <br />
Mutation이 완료되면 `onSettled`핸들러를 통해 쿼리를 다시 불러오고, 오류 발생 시 `isError`상태를 처리할 수 있다.<br />

## 캐시를 직접 조작하는 Optimistic Update
---
캐시를 직접 조작하는 Optimistic Update는 `onMutate` 핸들러를 사용하여 적용된다. <br />
이 방식은 주로 여러 컴포넌트에서 데이터가 변경될 때 유용하다. <br />

예를 들면, Todo 항목을 업데이트할 때 다음과 같이 사용할 수 있다.<br />
```jsx
const queryClient = useQueryClient();

useMutation({
  mutationFn: updateTodo,
  onMutate: async (newTodo) => {
    // 이전 데이터 스냅샷
    const previousTodos = queryClient.getQueryData(['todos']);

    // Optimistic Update
    queryClient.setQueryData(['todos'], (oldTodos) => [...oldTodos, newTodo]);

    // 롤백을 위한 context 반환
    return { previousTodos };
  },
  onError: (error, newTodo, context) => {
    // 에러 발생 시 롤백
    queryClient.setQueryData(['todos'], context.previousTodos);
  },
  onSettled: () => {
    // 항상 완료 후 쿼리 무효화
    queryClient.invalidateQueries({ queryKey: ['todos'] });
  },
});
```
이 예시에서 `onMutate` 핸들러는 새로운 Todo를 Optimistic하게 추가하고, `onError` 핸들러는 <br />
에러 발생 시 이전 데이터로 롤백한다. `onSettled` 핸들러는 항상 완료 후 쿼리를 다시 불러오는 역할을 한다.<br />

## 결론
---
Optimistic Update는 사용자가 데이터 변경을 즉시 확인할 수 있도록 하는 중요한 기술이다. <br />
React Query를 사용하면 간편하게 캐시를 조작하거나 UI를 업데이트할 수 있어, 사용자 경험을 개선하는 데 <br />
큰 도움이 된다. 각 상황에 맞게 적절한 방식을 선택하여 사용하면 좋을 것 같다. <br />

[공식문서](https://tanstack.com/query/latest/docs/framework/react/guides/optimistic-updates#optimistic-updates)