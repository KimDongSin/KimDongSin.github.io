---
layout: post
title: 이벤트 버블링(Event Bubbling)과 캡쳐링(Event Capturing)
description: 이벤트 버블링(Event Bubbling)과 캡쳐링(Event Capturing)을 알아보자.
author: dongsin
date: 2024-05-02 09:30 +09:00
categories: [Javascript]
tags: [Javascript]
pin: false
math: true
mermaid: true
image:
  path: https://arielfuggini.com/static/29a9f86a9bd7efd96ee9ce8b13124303/a41d1/javascript.jpg
---


## 이벤트 버블링(Event Bubbling)과 캡쳐링(Event Capturing)

이벤트 버블링과 캡쳐링은 이벤트가 DOM트리를 통해 전파되는 방식이다.

<br />

## 이벤트 버블링(Event Bubbling)

<img width="50%" src="https://joshua1988.github.io/images/posts/web/javascript/event/event-bubble.png" />

이벤트가 발생한 요소에서 시작하여 최상위 요소까지 올라가는 과정이다.<br />
즉, 이벤트가 타겟 요소에서 발생한 후 최상위 요소까지 거슬러 올라간다. <br />



<br />


## 이벤트 캡쳐링(Event Capturing)

<img width="50%" src="https://velog.velcdn.com/images/o1011/post/c31cb585-bd94-4066-a784-41afae997c0f/image.png" />

이벤트가 최상위 요소에서부터 시작하여 이벤트가 발생한 요소까지 내려가는 과정이다.<br />
즉, 이벤트가 타겟 요소에서 발생하기 전에 최상위 요소에서 시작하여 타겟 요소까지 전파된다.<br />


<br />


### 이벤트 버블링과 이벤트캡쳐링 코드로 확인하기
```js
const parent = document.getElementById('parent');
const child = document.getElementById('child');

// 버튼에 클릭 이벤트 추가
child.addEventListener('click', function(event) {
  console.log('버튼 클릭!');
  // 이벤트가 상위 요소로 전파됨
  console.log('이벤트 버블링: ', event.currentTarget.id);
});

// 부모 요소에 클릭 이벤트 추가
parent.addEventListener('click', function(event) {
  console.log('부모 요소 클릭!');
  // 이벤트가 버블링되는 순서 확인
  console.log('이벤트 버블링: ', event.currentTarget.id);
});
```


## 이벤트 전파 방지방법
### **stopPropagation**과 **preventDefault** 이 두가지로 이벤트 전파를 방지할 수 있다.<br />
stopPropagation메소드를 버블링이나 캡쳐링 단계에서 이벤트 전파를 막을 수 있다. <br />
<br />
또한, 특정 요소에서 발생한 이벤트가 해당 요소의 부모/자식요소로 계속 전달되는 것을 막아<br />
다른 요소들이 해당 이벤트를 감지하지 못하도록 한다.<br />



## 결론
이벤트 버블링과 캡쳐링은 이벤트가 DOM트리를 통해 전파되는 방식이며, <br />
이를 활용하여 이벤트를 효율적으로 처리할 수 있다.<br />

주의할 점은 이벤트 캡쳐링은 거의 사용되지 않으며, 대부분은 이벤트 버블링을 사용한다.

간단 요약하자면<br />
이벤트 버블링은 하위에서 상위로, 이벤트 캡쳐링은 상위에서 하위로 가는 과정이다.<br />
이벤트 전파 방지는 **stopPropagation**과 **preventDefault**를 활용한다.
