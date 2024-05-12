---
layout: post
title: 클로저(Closure)란 무엇인가?
description: 클로저(Closure)를 알아보자.
author: dongsin
date: 2024-05-12 00:30 +09:00
categories: [Javascript]
tags: [Javascript]
pin: false
math: true
mermaid: true
image:
  path: https://arielfuggini.com/static/29a9f86a9bd7efd96ee9ce8b13124303/a41d1/javascript.jpg
---

## 클로저(Closure)란 무엇인가?
***
> 클로저는 JS에서 중요한 개념 중 하나로, 함수와 선언된 렉시컬 환경의 조합을 나타낸다. <br />

클로저는 외부 함수에서 선언된 변수에 접근할 수 있는 내부 함수를 가리키며, 이를 통해 <br />
외부 함수의 변수를 보호하고 관리 할 수 있다. <br />
<br />

### 클로저의 개념
***
클로저는 함수가 정의될 때 함수 내부에서 사용되는 변수와 그 변수가 선언된 <br />
렉시컬 환경을 기억하는 특정이 있다.  <br />

이로 인해 외부 함수의 실행이 종료된 이후에도 내부 함수가 외부 함수의 변수에 접근할 수 있다.<br />

이러한 동작 방식은 클로저가 생성되는 원리로, <br />
외부 함수와 내부 함수의 스코프 체인을 통해 변수에 접근 할 수 있게 된다. 

<br />

### 클로저의 활용
***
#### 데이터 은닉
클로저를 사용하여 변수를 외부에 노출 시키지않고도 보호하고 관리할 수 있다. <br />
이를 통해 프라이빗(private)한 변수를 만들고 외부에서의 직접적인 접근을 제한할 수 있다. <br />

#### 콜백 함수
클로저를 사용하여 콜백 함수에서 변수에 접근할 수 있다. <br />
이를 통해 비동기적인 작업을 수행하고 그 결과를 안전하게 처리할 수 있다. <br />

#### 모듈 패턴
클로저를 사용하여 모듈을 구현할 수 있다.<br />
모듈은 관련된 변수와 함수를 묶어서 캡슐화하고 필요한 경우에만 외부에 노출시켜서<br />
코드의 유지보수성을 높이고 전역 스코프의 오염을 방지할 수 있다. <br />

<br />

### 클로저의 예시코드
***
```js
function outerFunction() {
  let outerVariable = '외부 함수에서 온 변수';
  
  function innerFunction() {
    console.log(outerVariable); // outerVariable에 접근
  }
  
  return innerFunction;
}

const innerFunc = outerFunction();
innerFunc(); // 결과: "외부 함수에서 온 변수"

```

위의 코드에서 `outerVariable`은 외부 함수 `outerFunction`내에서 선언된 변수이다 <br />
클로저를 통해 `innerFunction`이 외부 함수의 변수에 접근할 수 있다. <br />
따라서 실행 결과는 "외부 함수에서 온 변수"가 출력 된다. <br />

<br />

## 결론
***
클로저를 통해 외부 함수의 변수에 안전하게 접근하고 관리하는 방법을 알아보았다.<br />

클로저를 사용하면 변수를 보호하고 필요한 경우에만 접근할 수 있도록 제어할 수 있다. <br />
이는 데이터 은닉을 구현하는데 매우 유용하고 코드의 안정성과 유지보수성을 높일 수 있다. <br />

클로저를 이해하고 적절히 활용하면 JS에서 더욱 효율적이고 안전한 코드를 작성할 수 있다. <br />
