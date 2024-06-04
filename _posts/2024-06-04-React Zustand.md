---
layout: post
title: Zustand 사용법
description: Zustand를 알아보자.
author: dongsin
date: 2024-06-04 00:10 +09:00
categories: [React]
tags: [React]
pin: false
math: true
mermaid: true
image:
  path: https://github.com/pmndrs/zustand/raw/main/bear.jpg
---

### 전역 상태 관리의 Zustand
---

프론트엔드 개발에서 상태 관리는 매우 중요한 부분이다. <br />
리액트 애플리케이션에서 상태를 효과적으로 관리하기 위해 다양한 도구들이 존재하지만,<br />
최근 주목받고 있는 도구 중 하나가 바로 Zustand이다.<br />
<br />

### Zustand란 무엇인가?
---
Zustand는 가볍고 빠른 상태 관리 라이브러리로, 리액트와 함께 사용되도록 설계되었다.<br />
간단한 API와 최소한의 코드로 상태 관리를 가능하게 하며, <br />
Redux와 같은 기존 상태 관리 라이브러리의 복잡성을 줄여준다. <br />

Zustand는 `react`와 `@babel/preset-react`를 사용하여 만들어졌으며, 직관적인 사용법 덕분에<br />
빠르게 배우고 적용할 수 있다.<br />


### Zustand 설치하기
---
npm 또는 yarn을 사용하여 쉽게 설치할 수 있다.



```
npm install zustand 혹은 yarn add zustand

```

### 기본 사용법
---

Zustand의 기본 사용법은 매우 간단하다. 먼저, 상태를 정의하고 이를 사용하는 코드를 작성해보자.
```jsx
import create from 'zustand'

// 상태 생성
const useStore = create(set => ({
  count: 0,
  increase: () => set(state => ({ count: state.count + 1 })),
  decrease: () => set(state => ({ count: state.count - 1 }))
}))

function Counter() {
  const { count, increase, decrease } = useStore()

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={increase}>Increase</button>
      <button onClick={decrease}>Decrease</button>
    </div>
  )
}

export default Counter

```

위의 예시 코드에서는 create 함수를 사용하여 상태를 정의하고, useStore 훅을 통해 상태를 사용하고 있다. <br />`increase`와 `decrease` 함수는 상태를 업데이트하는 함수들로, set 함수를 사용하여 상태를 변경한다.
<br />

### 더 복잡한 상태 관리
---
Zustand는 간단한 상태 관리뿐만 아니라, 복잡한 상태 관리도 쉽게 처리할 수 있다.<br />
예를 들어, 비동기 작업이나 미들웨어를 추가할 수 있다.<br />

```jsx
import create from 'zustand'
import { devtools, persist } from 'zustand/middleware'

// 비동기 작업을 위한 상태 생성
const useStore = create(devtools(persist((set, get) => ({
  user: null,
  fetchUser: async (id) => {
    const response = await fetch(`/api/user/${id}`)
    const user = await response.json()
    set({ user })
  }
}), { name: 'user-storage' })))

function User() {
  const { user, fetchUser } = useStore()

  React.useEffect(() => {
    fetchUser(1)
  }, [fetchUser])

  return (
    <div>
      {user ? <h1>{user.name}</h1> : <h1>Loading...</h1>}
    </div>
  )
}

export default User

```

위 예시에서는 `devtools`와 `persist` 미들웨어를 사용하여 상태를 관리하고, <br />
비동기 작업을 통해 데이터를 가져오고 있다. 이러한 기능들은 Zustand를 더욱 강력하게 만들어준다.

### 결론
---
Zustand는 단순하면서도 강력한 상태 관리 라이브러리로, 리액트에서의 상태 관리를 한층 쉽게 만든다.<br />
간단한 API와 다양한 확장 기능을 통해 개발자들이 더욱 효율적으로 상태를 관리할 수 있도록 돕는다.<br />


[Zustand 공식문서](https://docs.pmnd.rs/zustand/getting-started/introduction)