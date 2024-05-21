---
layout: post
title: React Router v5, v6방식 차이점
description: React Router v5, v6방식을 알아보자.
author: dongsin
date: 2024-05-21 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/chanyoungcoding/post/3889bf01-12ab-4cd2-8fd3-5d82750c1846/image.png
---

## React Router DOM
> React Router는 React에서 페이지 라우팅을 구현하기 위한 표준라이브러리이다.

SPA에서 페이지 간 전환을 관리하고, URL경로에 따라 적절한 컴포넌트를 렌더링할 수 있게 해준다.


### 라우팅이란?
어떤 경로에 대해서 무엇을 해줄지를 맵핑해 주는 것 <br />
SPA에서 여러 페이지를 효과적으로 관리할 수 있게 도와준다.

### SPA(Single Page Application)
한 번 로드된 후, 전체 페이지 새로고침이 없이 콘텐츠를 동적으로 바꾸는 것이다.


## 사용방법
---

#### 주요 컴포넌트와 훅
`BrowserRouter` : HTML5 히스토리 API를 사용하여 URL을 관리하는 라우터이다. 주로 최상위 컴포넌트를 감싸는데 사용됨. <br />
`Routes` : 여러 라우트를 감싸는 컨테이너이고, `Route`는 특정 경로에 대해 렌더링할 컴포넌트를 정의한다. <br />
`Link` : HTML의 `<a>`태그와 유사하게 동작하지만, 페이지 전체를 새로고침하지 않고도 경로를 변경할 수 있다. <br />
`useNavigate` : 지정한 경로로 페이지를 이동시킨다.
`useParams` : URL 경로에 포함된 동적 파라미터에 접근할 때 사용한다.

### v5 버전 방식
```jsx
function App() {
  return (
    <BrowserRouter basename="/app">
      <Routes>
        <Route path="/" /> {/* 👈 Renders at /app/ */}
      </Routes>
    </BrowserRouter>
  );
}
```

React Router DOM v5버전까지는 이런 방식으로 사용하였지만 v6버전이 업데이트되면서<br />
추가기능이 생겼다.


### v6 버전 방식
```jsx

const router = createBrowserRouter([
  {
    path: "/",
    element: <HomePage />,
  },
  {
    path: "/posts",
    element: <PostListPage />,
  },
  {
    path: "/posts/:postId", // 동적라우터 이름은 명시적으로 쓸 것.
    element: <PostDetailPage />,
  },
]);

export default router;

```

v6버전에서는 위와 같이 라우터를 관리한다.


## loader 사용법
`loader`는 컴포넌트가 렌더링되기 전에 데이터를 로드할 수 있게 해준다. <br />
`useLoaderData`훅을 사용하여 로드된 데이터를 컴포넌트 내에서 사용할 수 있다.<br />

```jsx
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import HomePage from "./pages/HomePage";
import PostListPage from "./pages/PostListPage";
import PostDetailPage from "./pages/PostDetailPage";

const router = createBrowserRouter([
  {
    path: "/",
    element: <HomePage />,
  },
  {
    path: "/posts",
    element: <PostListPage />,
    loader: async () => {
      const response = await fetch("/api/posts");
      const posts = await response.json();
      return posts;
    },
  },
  {
    path: "/posts/:postId",
    element: <PostDetailPage />,
    loader: async ({ params }) => {
      const response = await fetch(`/api/posts/${params.postId}`);
      const post = await response.json();
      return post;
    },
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;

```

```jsx
import { useLoaderData } from "react-router-dom";

function PostListPage() {
  const posts = useLoaderData();

  return (
    <div>
      <h1>Post List</h1>
      <ul>
        {posts.map(post => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}

export default PostListPage;
```

## 결론

React Router DOM은 SPA에서 CSR 라우팅을 효과적으로 관리할 수 있게 해주는 라이브러리이다.<br />
최선버전 v6에서는 더욱 간결하고 편리한 기능을 제공하며, 데이터 로딩, 라우팅 구성 등이 개선되었다. <br />


[React-Router-DOM 공식문서 링크](https://reactrouter.com/en/main)