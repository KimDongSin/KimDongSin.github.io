---
layout: post
title: parentNode와 parentElement의 차이점
description: parentNode와 parentElement의 차이점을 알아보자.
author: dongsin
date: 2024-05-01 18:30 +09:00
categories: [Javascript]
tags: [Javascript]
pin: false
math: true
mermaid: true
image:
  path: https://arielfuggini.com/static/29a9f86a9bd7efd96ee9ce8b13124303/a41d1/javascript.jpg
---

JavaSrcipt에서 DOM을 다룰 때, 요소의 부모를 찾는데 사용되는 두가지 속성이 있다.<br />
**parentNode**와 **parentElement** 이 두가지 속성은 비슷해 보일 수 있지만, 실제로는 약간의 차이가 있다.<br />
오늘은 이 차이점에 대해서 알아보겠다.

## parentNode
**parentNode** 속성은 요소의 부모 노드를 반환한다. 이 부모 노드는 다양한 종류일 수 있다. <br />
예를 들어, 요소의 부모가 **div**일수도 있고, **body**일 수도 있으며, 혹은 더 나아가서 **html**일 수도 있다.<br />

```js
const parent = element.parentNode;
```

만약 요소의 부모가 없다면(예를 들어 문서의 최상위 요소인 경우), **parentNode**는 **null**을 반환한다.<br />


<br />

## parentElement
**parentElement** 속성은 요소의 부모 엘리먼트를 반환한다. 이것은 요소의 부모 중 엘리먼트 노드인 것만을 반환한다.
즉, 요소의 부모가 엘리먼트가 아니라 텍스트 노드나 주석 노드 등 다른 노드 유형이라면<br />
**parentElement**는 **null**을 반환한다.

```js
const parent = element.parentElement;
```

**parentElement**는 요소가 엘리먼트 노드일 때 특히 유용하다.<br />
요소 자체가 다른 유형의 노드일수도 있으므로 **parentElement**는 부모가 엘리먼트임을 보장한다.


<br />

## 결론
정리하자면, **parentNode**는 요소의 부모 노드를 반환하는 반면 **parentElement**는 엘리먼트 노드인 부모를 반환한다.<br />
이 차이점을 이해하면 DOM을 조작할 때 보다 정확하게 코드를 작성할 수 있다.