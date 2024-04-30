---
layout: post
title: Javascript matches, join메서드
description: Javascript matches, join메서드를 알아보자.
author: dongsin
date: 2024-04-29 18:30 +09:00
categories: [Javascript]
tags: [Javascript]
pin: false
math: true
mermaid: true
image:
  path: https://arielfuggini.com/static/29a9f86a9bd7efd96ee9ce8b13124303/a41d1/javascript.jpg
---

## matches()

> matches() 메서드는 주어진 선택자에 해당하는 요소가 현재 요소와 일치하는지 여부를 확인한다.

이 메서드는 boolean값으로 반환한다.


```js
const element = document.querySelector('.example-class');
const isMatch = element.matches('.another-class');
console.log(isMatch); // true 또는 false 출력
```

이 메서드는 주로 CSS스타일링이나 이벤트 위임 등과 함께 사용한다. <br />
예를 들어, 특정 요소가 이벤트를 처리해야 할 때 해당 요소에 대한 이벤트 핸들러를 등록하기 전에<br />
요소가 일치하는지 먼저 확인 할 수 있다.



## join()

> join() 메서드는 배열의 모든 요소를 하나의 문자열로 결합하여 반환한다. <br />
> 이 문자열은 구분자로 구분된 요소들의 시퀀스이다.

반환 값은 모든배열 요소를 결합한 문자열이다.

```js
const fruits = ['사과', '바나나', '오렌지'];
const result = fruits.join(', '); // 구분자로 쉼표와 공백 사용
console.log(result); // "사과, 바나나, 오렌지" 출력
```
<br />

***
## 개인과제를 통해서 배운 점


### matches() 응용코드

```js
cardList.addEventListener("click", handleClickCard);

  // 이벤트 위임: 하위요소에서 발생한 이벤트를 상위요소에서 처리하도록 해줍니다.
  function handleClickCard({ target }) {
    // 카드 외 영역 클릭 시 무시
    if (target === cardList) return;

    if (target.matches(".movie-card")) {
      alert(`영화 id: ${target.id}`);
    } else {
      // 카드의 자식 태그 (img, h3, p) 클릭 시 부모의 id로 접근
      alert(`영화 id: ${target.parentNode.id}`);
    }
  }
```


### join() 응용코드

```js
const cardList = document.querySelector("#card-list");
  cardList.innerHTML = movies
    .map(
      (movie) => `
          <li class="movie-card" id=${movie.id}>
              <img src="https://image.tmdb.org/t/p/w500${movie.poster_path}" alt="${movie.title}">
              <h3 class="movie-title">${movie.title}</h3>
              <p>${movie.overview}</p>
              <p>Rating: ${movie.vote_average}</p>
          </li>`
    )
    .join("");
```


다른 분의 movieSite개인과제 프로젝트를 보고 요소추가를 할 때<br />
matches와 join 메서드를 응용해서 이런식으로도 할 수 있다는 것을 깨달았다.