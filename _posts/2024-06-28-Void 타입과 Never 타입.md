---
layout: post
title: void 타입과 never 타입
description: void, never 타입 개념정리
author: dongsin
date: 2024-06-28 12:00 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---

## void 타입
---
void 타입은 함수의 반환 타입으로 사용되며, 함수가 반환할 값이 없음을 나타낸다. <br />
JavaScript에서는 undefined를 반환하는 함수의 타입을 void로 정의할 수 있다.<br />

### void 특징
---

* 함수가 어떤 값도 반환하지 않음을 의미한다.
* 변수에 void 타입을 명시적으로 지정할 수 있지만, 일반적으로는 함수의 반환 타입으로 사용된다.

### 예시코드
---
```tsx
function greet(): void {
    console.log('Hello!');
    // return; // 이 함수는 반환 타입이 void이므로 반환문이 없어도 된다.
}

let unusable: void = undefined; // 변수에 명시적으로 void 타입을 지정할 수 있다.
```

## never 타입
---
never 타입은 절대 발생할 수 없는 타입을 나타낸다. <br />
주로 예외나 무한 루프 등의 상황에서 함수가 정상적으로 종료되지 않을 때 사용된다.<br />

### never 특징
---

* 함수가 항상 예외를 던지거나 무한 루프에 빠지는 경우와 같이 절대로 정상적으로 종료되지 않는 상황을 나타낸다.
* 다른 모든 타입의 하위 타입으로, 어떤 타입에도 할당할 수 있다.

### 예시 코드
---
```tsx
function throwError(message: string): never {
    throw new Error(message);
}

function infiniteLoop(): never {
    while (true) {
        // 무한 루프
    }
}

let neverVariable: never; // 변수에 명시적으로 never 타입을 지정할 수 있다.
```

## void와 never 타입 비교
---
* void는 함수의 반환 타입으로 사용되며, 함수가 반환할 값이 없음을 명시한다.
* never는 함수가 절대로 정상적으로 종료되지 않는 상황을 나타내며, 예외 또는 무한루프와 같은 상황에서 사용된다.

### 적절한 사용처
---
* void는 함수가 값을 반환하지 않고 단순히 동작을 수행할 때 사용한다.
* never는 함수가 예외를 던지거나 무한 루프에 빠질 때 사용하며, 함수가 어떠한 상황에서도 정상적으로 반환될 수 없음을 명시적으로 표현할 때 유용하다.

## 결론
---
void 타입과 never 타입은 TypeScript에서 함수의 동작을 명확히 하고, 예외 상황을 처리하는 데 유용하게 사용된다.<br />
void는 함수가 반환할 값이 없음을 명시하고, never는 함수가 절대로 정상적으로 종료되지 않음을 나타낸다.<br />

[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)