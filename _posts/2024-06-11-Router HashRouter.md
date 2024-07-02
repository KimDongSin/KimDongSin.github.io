---
layout: post
title: ReactRouter HashRouter
description: HashRouter를 알아보자.
author: dongsin
date: 2024-06-11 00:10 +09:00
categories: [React]
tags: [ReactRouter]
pin: false
math: true
mermaid: true
image:
  path:  https://velog.velcdn.com/images/chanyoungcoding/post/3889bf01-12ab-4cd2-8fd3-5d82750c1846/image.png
---

## HashRouter란 무엇인가?
---
`HashRouter`는 URL의 해시(#) 부분을 사용하여 클라이언트 즉 라우팅을 관리한다. <br />
이는 브라우저의 기본 기능을 활용하여 페이지 새로고침 없이 URL 변경을 감지하고, <br />
해당 URL에 매핑된 컴포넌트를 렌더링한다.<br />

### 장점
---
* 서버 설정이 필요하지 않다.
* 간단한 설정으로 클라이언트 측 라우팅 구현 가능하다.
* 모든 브라우저에서 일관되게 동작한다.

### 예시 코드
---
`HashRouter`의 예시코드를 살펴보자.
```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import { HashRouter as Router, Route, Switch, Link } from 'react-router-dom';

const Home = () => <h2>Home Page</h2>;
const About = () => <h2>About Page</h2>;
const Contact = () => <h2>Contact Page</h2>;

const User = ({ match }) => <h2>User: {match.params.username}</h2>;

const App = () => (
  <Router>
    <div>
      <nav>
        <ul>
          <li><Link to="/">Home</Link></li>
          <li><Link to="/about">About</Link></li>
          <li><Link to="/contact">Contact</Link></li>
          <li><Link to="/user/johndoe">John Doe</Link></li>
        </ul>
      </nav>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/contact" component={Contact} />
        <Route path="/user/:username" component={User} />
      </Switch>
    </div>
  </Router>
);

ReactDOM.render(<App />, document.getElementById('root'));
```

## HashRouter의 장단점
---
### 장점
1. 해시 값을 사용하여 페이지를 관리하기 때문에 서버 설정이 불필요하다.
2. 해시 값으로 사용하기 때문에 컴포넌트 변경이 부드럽고 빠르다.

### 단점
1. 검색 엔진은 해시를 무시하므로, SEO에 불리하다.
2. 해시값을 사용하기 때문에 URL 구조가 깔끔하지 않다.


## 결론
---
SEO에 불리하지만 해시로 캐싱하여 사용하기에 컴포넌트 변경이 부드럽고 빠르다. <br />
검색 엔진이 필요없는 프로젝트라면 사용하면 좋을 것 같다. <br />

그리고 성능을 극한으로 올려줄 때 사용하면 도움이 될 것같다. <br />

[공식문서](https://reactrouter.com/en/main/router-components/hash-router#hashrouter)