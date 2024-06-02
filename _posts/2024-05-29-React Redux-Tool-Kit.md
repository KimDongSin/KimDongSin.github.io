---
layout: post
title: Redux ToolKit(RTK)
description: Redux ToolKit을 알아보자.
author: dongsin
date: 2024-05-29 00:10 +09:00
categories: [React]
tags: [Redux, Redux ToolKit]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/mywonhyuni/post/9a9f1694-1d20-4ff6-ad5f-892d4f8de9f5/image.png
---

## Redux Toolkit (RTK)란?
---
Redux Toolkit (RTK)은 Redux를 더욱 간편하고 효율적으로 작성할 수 있게 도와주는 도구이다.<br />
RTK는 설정을 간소화하고, 보일러 플레이트 코드를 줄여준다.<br />


## Redux ToolKit 주요개념
---
* configureStore
    * Redux store를 설정하는 간단한 방법이다.
    * 여러 개의 리듀서를 결합하고, Redux DevTools 및 기본 미들웨어 설정을 포함한다.
* createSlice
    * 액션 생성자와 리듀서를 동시에 정의할 수 있는 방법이다.
* createAsyncThunk
    * 비동기 로직을 처리하고, 액션 타입을 자동으로 생성하는 도구이다.
* createReducer
    * 보다 간단하고 직관적인 방식으로 리듀서를 작성할 수 있다.
* createAction
    *  액션 생성자를 쉽게 만들 수 있다.


## RTK 세팅
Redux ToolKit과 React-Redux를 설치한다.
```
npm install @reduxjs/toolkit react-redux
```

## 1. Store 생성
먼저 `configureStore`를 사용하여 스토어를 생성한다.

```js
// store.js
import { configureStore } from '@reduxjs/toolkit';
import todosReducer from './todosSlice';

const store = configureStore({
  reducer: {
    todos: todosReducer,
  },
});

export default store;

```

## 2. React-Redux 연결
Redux와 마찬가지로, `Provider`컴포넌트를 사용하여 스토어를 React에 연결한다.
```jsx
// main.jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import App from './App';
import store from './store';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

```

## 3. Slice 정의
`createSlice`를 사용하여 액션과 리듀서를 정의한다.
```js
// todosSlice.js
import { createSlice } from '@reduxjs/toolkit';
import { v4 as uuidv4 } from 'uuid';

const todosSlice = createSlice({
  name: 'todos',
  initialState: [],
  reducers: {
    addTodo: (state, action) => {
      state.push({ id: uuidv4(), text: action.payload });
    },
    deleteTodo: (state, action) => {
      return state.filter(todo => todo.id !== action.payload);
    },
  },
});

export const { addTodo, deleteTodo } = todosSlice.actions;
export default todosSlice.reducer;
```

## 4. 컴포넌트에서 Redux 사용
```jsx
// TodoList.jsx
import React, { useState } from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { addTodo, deleteTodo } from './todosSlice';

function TodoList() {
  const [newTodo, setNewTodo] = useState('');
  const todos = useSelector(state => state.todos);
  const dispatch = useDispatch();

  const handleAddTodo = () => {
    if (newTodo.trim() !== '') {
      dispatch(addTodo(newTodo));
      setNewTodo('');
    }
  };

  return (
    <div>
      <h1>Todo List</h1>
      <input
        type="text"
        value={newTodo}
        onChange={(e) => setNewTodo(e.target.value)}
      />
      <button onClick={handleAddTodo}>Add Todo</button>
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>
            {todo.text}
            <button onClick={() => dispatch(deleteTodo(todo.id))}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default TodoList;
```
<br />

## 결론
---
RTK는 Redux의 복잡함을 줄이고, 설정을 간소화하며, 보일러플레이트 코드를 줄이는데 큰 도움을 준다. <br />
`configureStore`, `createSlice`, `createAsyncThunk`등 다양한 도구를 제공하여<br />
효율적으로 상태관리를 할 수 있게 도와준다. RTK를 사용하여 더 간편하고 직관적으로 Redux를 사용하게 해준다.<br />

### 주요 개념정리
1. configureStore: 스토어 설정을 간소화한다.
2. createSlice: 액션과 리듀서를 동시에 정의한다.
3. React-Redux 연동: Provider로 스토어를 애플리케이션에 연결한다.

[RTK 공식문서](https://ko.redux.js.org/redux-toolkit/overview/)