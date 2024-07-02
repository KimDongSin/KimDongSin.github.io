---
layout: post
title: invalidateQueries
description: invalidateQueries 개념정리
author: dongsin
date: 2024-06-18 00:10 +09:00
categories: [ReactQuery]
tags: [React, ReactQuery]
pin: false
math: true
mermaid: true
image:
  path:  https://t1.kakaocdn.net/kakao_tech/image/2022/06/images/01.png
---

## invalidateQueries란?
리액트 쿼리에서 invalidateQueries는 캐시된 데이터를 무효화하고<br />
새로운 데이터를 다시 가져오도록 요청하는 메서드이다.<br />

### 사용해야 되는 상황
---
#### 데이터 변경 후 새로고침
예를 들어, 사용자가 데이터를 수정하고 나서 데이터를 새로고침해야 할 때 사용된다.<br />
이 경우 기존 쿼리 캐시를 무효화하고, 변경된 데이터를 다시 가져와서 UI를 업데이트한다.<br />

#### 실시간 데이터 업데이트
다른 사용자가 데이터를 변경할 경우, 새로운 데이터가 서버에 반영되어 <br />
UI가 실시간으로 업데이트되어야 할 때 사용될 수 있다. <br />
이 때 invalidateQueries를 사용하여 변경 사항을 즉시 반영할 수 있다. <br />

## 예시코드
---
```jsx
import React from 'react';
import { useQuery, useQueryClient } from 'react-query';

const fetchPosts = async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  if (!response.ok) {
    throw new Error('네트워크 오류 - 데이터를 가져올 수 없습니다.');
  }
  return response.json();
};

const Posts = () => {
  const queryClient = useQueryClient();

  const { data, isLoading, isError } = useQuery('posts', fetchPosts);

  const handleRefresh = async () => {
    await queryClient.invalidateQueries('posts');
  };

  if (isLoading) return <p>Loading...</p>;
  if (isError) return <p>Error fetching data...</p>;

  return (
    <div>
      <h2>Posts</h2>
      <button onClick={handleRefresh}>Refresh</button>
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

위의 예시코드에서 `handleRefresh` 함수는 `queryClient.invalidateQueries('posts')`를 호출하여<br />
'post'라는 쿼리를 무효화하고 새로운 데이터를 가져오도록 요청한다. <br />
이를 통해 사용자가 데이터를 갱신할 때 기존 데이터를 즉시 업데이트할 수 있다.<br />

## 결론
---
따라서, invalidateQueries는 리액트 쿼리에서 데이터 캐시 관리를 유연하게 제어하고, <br />
실시간으로 데이터를 업데이트 하는 데 유용한 기능이다.<br />
