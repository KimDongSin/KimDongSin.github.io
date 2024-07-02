---
layout: post
title: Mutation 이해와 활용
description: Mutation을 알아보자.
author: dongsin
date: 2024-06-17 00:10 +09:00
categories: [ReactQuery]
tags: [React, ReactQuery]
pin: false
math: true
mermaid: true
image:
  path:  https://t1.kakaocdn.net/kakao_tech/image/2022/06/images/01.png
---

## Mutation이란?
---
Mutation은 주로 DB를 업데이트하거나 변경하는 작업을 말한다. <br />
예를 들어, 새로운 데이터를 추가하거나 기존 데이터를 수정 또는 삭제할 때 사용된다. => (CUD)

### 주요 기능
---
* 데이터 수정, 생성, 삭제
* 비동기 작업 처리 및 성공 또는 실패 시 액션 실행
* 캐시 업데이트 및 반영

### Mutation 예시코드
---

```jsx
import React from 'react';
import { useMutation, useQueryClient } from 'react-query';

const createUser = async (newUser) => {
  const response = await fetch('https://jsonplaceholder.typicode.com/users', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(newUser),
  });

  if (!response.ok) {
    throw new Error('사용자 생성에 실패했습니다.');
  }

  return response.json();
};

const CreateUserForm = () => {
  const queryClient = useQueryClient();

  const mutation = useMutation(createUser, {
    onSuccess: (data) => {
      // 뮤테이션 성공 시, 캐시를 업데이트하여 UI를 갱신한다.
      queryClient.invalidateQueries('users'); // 'users' 쿼리 캐시 무효화
    },
  });

  const handleSubmit = async (event) => {
    event.preventDefault();
    const formData = new FormData(event.target);
    const newUser = {
      name: formData.get('name'),
      email: formData.get('email'),
    };

    try {
      await mutation.mutateAsync(newUser);
      console.log('사용자가 성공적으로 생성되었습니다.');
    } catch (error) {
      console.error('사용자 생성 오류:', error.message);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        이름:
        <input type="text" name="name" required />
      </label>
      <label>
        이메일:
        <input type="email" name="email" required />
      </label>
      <button type="submit" disabled={mutation.isLoading}>
        {mutation.isLoading ? '저장 중...' : '저장'}
      </button>
    </form>
  );
};

export default CreateUserForm;
```
### 주의사항
---
먼저, 주의사항으로는 const mutation = useMutation 이 부분은 프로젝트 규모가 커질수록 <br />
의미있는 작명을 할 필요가 있다. 이렇게 사용하면 다른 사람들이 뭐하는 코드인지 모르니 주의하자.<br />

### Mutation 활용
---
#### 캐싱 업데이트
뮤테이션 성공 시 `onSuccess` 핸들러를 통해 쿼리 캐시를 업데이트하고 UI를 갱신할 수 있다.

#### 비동기 처리
비동기 작업을 수행하며, 성공 또는 실패 시 적절한 처리를 수행할 수 있다.

#### 재사용성
여러 컴포넌트에서 동일한 뮤테이션을 사용하여 데이터 업데이트 로직을 표준화하고, 코드를 간소화할 수 있다.

## 결론
---
`mutation`은 리액트 쿼리에서 데이터 수정, 생성, 삭제를 간편하게 처리할 수 있는 기능이다. <br />
데이터베이스와의 상호작용을 통해 상태를 업데이트하고, 사용자 경험을 개선하는 데 중요한 역할을 한다. <br />
