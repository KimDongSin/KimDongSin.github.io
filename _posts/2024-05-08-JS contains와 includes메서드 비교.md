---
layout: post
title: contains와 includes메서드 비교
description: contains와 includes메서드 비교해보자.
author: dongsin
date: 2024-05-08 00:30 +09:00
categories: [Javascript]
tags: [Javascript]
pin: false
math: true
mermaid: true
image:
  path: https://arielfuggini.com/static/29a9f86a9bd7efd96ee9ce8b13124303/a41d1/javascript.jpg
---

## contains()란?

> 선택한 요소가 특정 부모요소에 속해 있는지 확인할 때 사용한다.

주로 특정요소를 선택하여 부모 요소가 해당 요소를 가지고 있는지 boolean으로 확인할 수 있다. <br />
하나의 엘리먼트가 특정 클래스를 포함하고 있는지 검증할 때도 사용할 수 있다.

```js
const h1 = document.querySeletor("h1");

const actionClass = "action";

if(h1.classList.contains(actionClass)){ // h1요소에 action클래스가 존재한다면 true
    h1.classList.remove(actionClass);
}else{ // false
    h1.classList.add(actionClass);
}

```

**해당노드B가 지정 노드 A의 자손인지 여부를 판별해서 맞으면 true 아니면 false를 반환한다.**<br />
위와 같이 classList 혹은 엘리먼트 등에 활용가능하다.


노드 기준이 아닌 배열기준에서는 includes메서드가 존재한다.


<br />

## includes()란?
> 배열이나 문자열에 특정한 값을 포함하는지 여부를 확인하는 메서드다.

contains()메서드와 마찬가지로 기능은 비슷하지만 노드 메서드가 아닌 배열 메서드이고, boolean값을 반환한다.

```js
const arr = [1, 2, 3, 4, 5];

console.log(arr.includes(3)); // 출력: true
console.log(arr.includes(6)); // 출력: false

```

## 결론
contains()메서드와 includes메서드는 둘 다 값을 포함하고 있는지 여부를 판별하지만<br />
**contains()는 노드메서드**이고, **includes()는 배열메서드**이다.