---
layout: post
title: React Redux란
description: React Redux를 알아보자.
author: dongsin
date: 2024-05-28 00:10 +09:00
categories: [React]
tags: [styled-components]
pin: false
math: true
mermaid: true
image:
  path: https://vietnamlife.info/wp-content/uploads/2023/05/redux-logo-landscape.png
---

## Redux란?
---
Redux는 상태관리를 간편하게 해주는 전역상태관리 라이브러리이다.<br />
상태(state)란 데이터의 현재 상태를 의미하며, 컴포넌트 간의 데이터 공유, 상태 변경 등을 <br />
효율적으로 관리 할 수 있게 해준다. <br />

## Redux의 주요 개념
---
* Store
    * 상태를 담고 있는 객체이다. Redux는 단일 스토어를 가진다.
* Action
    * 상태에 어떤 변화가 필요할 때 **dispatch**되는 객체이다.
    * action의 `type` 속성을 필수로 가지며, 추가로 상태 변경에 필요한 데이터를 포함할 수 있다.
    * action은 `payload` 속성도 가지고 있고, 이 것은 상태 변경에 필요한 데이터를 포함한다.
* Reducer
    * 액션을 받아 상태의 변화를 처리하는 함수이다.
    * 현재 상태(state)와 액션(action)을 인자로 받아 새로운 상태를 반환한다
* Dispatch
    * 액션을 스토어(store)에 보내는 함수이다.
* Subscribe
    * 스토어의 상태가 변경될 때마다 특정 콜백 함수를 실행한다.

## Redux 세팅
---
Redux와 React-Redux를 설치한다.
```
npm install redux react-redux
```

## 1. Store생성
먼저 Redux를 사용하기 위해 세팅해보자.  <br />
스토어는 리듀서를 사용하여 생성한다.<br />
```js
// store.js
import { createStore } from 'redux';
import todoReducer from './reducers';

const store = createStore(todoReducer);

export default store;

```

## 2. React-Redux 연결
React-Redux의 `Provider` 컴포넌트를 App에 감싸주어 스토어를 리액트에 연결한다.
```js
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
<br />

## 예시코드
---
TodoList를 예시코드로 살펴보자. <br />

### 1. action과 action creator정의
action은 state를 변경하는 데 필요한 정보를 담는다.

```js
export const ADD_TODO = 'ADD_TODO';
export const DELETE_TODO = 'DELETE_TODO';

// 액션 생성자
export const addTodo = (todo) => ({
  type: ADD_TODO,
  payload: todo,
});

export const deleteTodo = (id) => ({
  type: DELETE_TODO,
  payload: id,
});

```

TodoList에서 추가와 삭제를 수행하는 action을 정의했다.

### Reducer 정의
리듀서는 액션을 받아 상태를 어떻게 변경할지 정의한다.
```js
import { ADD_TODO, DELETE_TODO } from './actions';

const initialState = {
  todos: [],
};

const todoReducer = (state = initialState, action) => {
  switch (action.type) {
    case ADD_TODO:
      return {
        ...state,
        todos: [...state.todos, action.payload],
      };
    case DELETE_TODO:
      return {
        ...state,
        todos: state.todos.filter(todo => todo.id !== action.payload),
      };
    default:
      return state;
  }
};

export default todoReducer;

```

## 간단 요약
---
* action 생성자
    *  `addTodo`와 `deleteTodo`는 각각 새로운 할 일을 추가하고 기존 할 일을 삭제하는 액션 객체를 반환한다.
* payload 전달
    * `addTodo` 액션 생성자는 새로운 할 일 객체를 `payload`로 전달하고
    * `deleteTodo` 액션 생성자는 할 일의 ID를 `payload`로 전달한다.
* Reducer
    * `ADD_TODO`와 `DELETE_TODO` 액션 타입에 따라 `payload` 데이터를 사용해서 상태를 업데이트 한다.


## 결론
Redux는 전역상태관리 라이브러리이다. <br />
Redux는 상태 관리를 더욱 체계적이고 효율적으로 만들기 위한 도구이다.<br />
이를 통해 state의 일관성을 유지하고, 예측 가능한 방식으로 상태를 변경할 수 있다.<br />

### 주요 개념
* Store: 애플리케이션의 상태를 보관하는 단일 객체.
* Action: 상태 변경을 요청하는 객체로, type과 payload 속성을 포함.
* Reducer: 액션을 받아 상태를 변경하는 순수 함수.
* Dispatch: 액션을 스토어로 보내는 함수.
* Subscribe: 스토어의 상태 변경을 감지하고 특정 콜백 함수를 실행.

[Redux 공식문서](https://ko.redux.js.org/introduction/getting-started/)

