---
layout: post
title: DocumentFragment란?
description: DocumentFragment를 알아보자.
author: dongsin
date: 2024-05-07 00:30 +09:00
categories: [Javascript]
tags: [Javascript]
pin: false
math: true
mermaid: true
image:
  path: https://arielfuggini.com/static/29a9f86a9bd7efd96ee9ce8b13124303/a41d1/javascript.jpg
---

## DocumentFragment란?

**DocumentFragment**는 실제 DOM이 추가되기 전에 여러 DOM노드를 메모리상에서 그룹화하는데 사용된다. <br />
일종의 가상 컨테이너 역할을 한다. <br />
<br />
이는 DOM을 조작할 때 브라우저가 리렌더링 하지않고도 여러 변경사항을 일괄적으로 적용할 수 있게 해준다.

### 왜 사용해야 되는가?

#### 1. 성능향상
DOM을 조작할 일이 많을 때 **DocumentFragment**를 사용하여 여러 DOM요소를 메모리상에서<br />
일괄 처리함으로써 성능을 향상 시킬 수 있다.

#### 2. 코드 가독성 향상
**DoucmentFragment**를 사용하면 관련 DOM요소들을 하나로 그룹화 할 수 있어서 코드 가독성을 높힐 수 있다.


<br />

## 코드비교

### DocumentFragment를 사용하지 않은 코드

```js
// 일반 적인 요소추가 방식
const items = ['사과', '바나나', '딸기'];
const list = document.getElementById('myList');

items.forEach(item => {
    const li = document.createElement('li');
    li.textContent = item;
    list.appendChild(li); // 리스트에 새로운 아이템 추가
});

```

먼저 **DocumentFragment**를 사용하지 않고 아이템요소를 추가한 코드이다. <br />
이 코드에서는 아이템이 추가될 때마다 브라우저가 리렌더링을 하기때문에 성능저하가 발생할 수 있다.

<br />

### DocumentFragment 사용한 코드

```js
const items = ['사과', '바나나', '딸기'];
const list = document.getElementById('myList');
const fragment = document.createDocumentFragment();

items.forEach(item => {
    const li = document.createElement('li');
    li.textContent = item;
    fragment.appendChild(li); // DocumentFragment에 아이템 추가
});

list.appendChild(fragment); // 실제 DOM에 DocumentFragment 추가


```

위의 코드에서는 DocumentFragment를 생성하고,<br />
각 아이템을 DocumentFragment에 추가한 후, 한 번에 DocumentFragment를 실제 DOM에 추가한다.

<br />

## 결론

위와 같이 DocumentFragment를 사용하게 되면 <br />
DocumentFragment객체를 사용하면 최초 한번만 DOM에 접근하고 같은 결과를 가져오게 된다.


복잡한 DOM조작이 필요한 작업에서는 사용해주는 게 좋을 것 같다.
