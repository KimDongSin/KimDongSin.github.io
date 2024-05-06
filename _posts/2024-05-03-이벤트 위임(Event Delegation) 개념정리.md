---
layout: post
title: 이벤트 위임(Event Delegation) 개념정리
description: 이벤트 위임(Event Delegation)을 알아보자.
author: dongsin
date: 2024-05-03 00:30 +09:00
categories: [Javascript]
tags: [Javascript]
pin: false
math: true
mermaid: true
image:
  path: https://arielfuggini.com/static/29a9f86a9bd7efd96ee9ce8b13124303/a41d1/javascript.jpg
---

## 이벤트 위임(Event Delegation)
> 이벤트 위임은 이벤트 버블링과 캡쳐링이 선행되어야 한다.
<br />

이벤트 위임은 하위 요소에 각각 이벤트를 붙이지 않고, 상위 요소에서 하위 요소의 이벤트를 제어하는 방식이다.

<br />

## 이벤트 위임의 장점

### 메모리 소비 감소
> 이벤트 위임을 사용하면 많은 수의 이벤트 핸들러를 등록하는 것을 줄일 수 있다.

### 동적 요소 처리
> 동적으로 생성되는 요소에 대해서도 이벤트를 처리할 수 있다. <br />
새로운 요소가 추가되더라도 부모 요소에만 이벤트 핸들러를 등록하면 되므로, 코드를 유지보수하기 수월해진다.

<br />

## 예시코드

```
<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
const list = document.querySelector('ul');

list.addEventListener("click", (e) => {
  if (e.target.tagName === "LI") {
    console.log(e.target.innerText);
  }
});

```

ul태그를 클릭하면 li요소가 아니면 이벤트를 발생시키지 않는다. <br />
이처럼 부모요소에서 이벤트를 추가하고도 해당 이벤트가 발생한 자식요소에서 처리하는 패턴이다.

<br />

## 결론

이벤트 위임은 자바스크립트에서 효율적인 이벤트 처리 방법 중 하나이다. <br />
코드의 유지보수성을 높이고 성능 향상도 시킬 수 있으므로, 중요한 기법 중 하나이다.


