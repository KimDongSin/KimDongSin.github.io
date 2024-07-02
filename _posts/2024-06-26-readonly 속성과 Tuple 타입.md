---
layout: post
title: readonly 속성과 Tuple 타입
description: readonly 속성과 Tuple 타입 개념정리
author: dongsin
date: 2024-06-26 12:00 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---

## readonly 속성
---
readonly 속성은 객체나 배열의 요소를 수정할 수 없도록 만드는 기능이다. <br />
이를 통해 데이터의 불변성을 보장할 수 있다.<br />

### readonly 속성 예시
---
```tsx
type User = {
  readonly id: number;
  name: string;
};

const user: User = { id: 1, name: 'Alice' };
console.log(user.id); // 1

user.name = 'Bob'; // 정상적으로 작동
// user.id = 2; // 오류: 읽기 전용 속성이기 때문에 'id'에 할당할 수 없다.
```
위 예시에서 User 타입의 id 속성은 readonly로 선언되어 수정할 수 없다. <br />
이를 통해 id 속성의 불변성을 보장할 수 있다.<br />

### readonly 배열 예시
```tsx
const numbers: readonly number[] = [1, 2, 3];
console.log(numbers[0]); // 1

// numbers.push(4); // 오류: 읽기 전용 배열에 요소를 추가할 수 없다.
```
이 예시에서는 readonly 배열을 선언하여 배열의 요소를 수정하거나 추가할 수 없게 한다. <br />
이를 통해 배열의 불변성을 유지할 수 있다.<br />

## Tuple(튜플) 타입이란?
---
Tuple 타입은 고정된 개수의 요소를 가지며 각 요소의 타입이 지정된 배열을 의미한다. <br />
Tuple을 사용하면 배열의 특정 위치에 특정 타입의 값이 있어야 함을 보장할 수 있다.<br />

### Tuple 타입 예시코드
```tsx
let person: [string, number];
person = ['Alice', 30]; // 정상적으로 작동

// person = [30, 'Alice']; // 오류: '[number, string]' 형식은 '[string, number]' 형식에 할당할 수 없다.
```

위 예시에서 person 변수는 첫 번째 요소로 문자열을, 두 번째 요소로 숫자를 가지는 Tuple로 선언되었다.<br />
요소의 타입과 순서를 정확하게 맞춰야 한다.<br />

### readonly와 Tuple을 활용한 함수
```tsx
type Coordinate = readonly [number, number];

const move = (coord: Coordinate, dx: number, dy: number): Coordinate => {
  return [coord[0] + dx, coord[1] + dy];
};

const start: Coordinate = [0, 0];
const end: Coordinate = move(start, 5, 5);

console.log(end); // [5, 5]
// start[0] = 10; // 오류: 읽기 전용 속성이기 때문에 '0'에 할당할 수 없다.
```
위 예시에서 Coordinate 타입은 readonly Tuple로 선언되어, move 함수 내에서 새로운 좌표를 계산하여 반환한다.<br />
start 좌표는 수정할 수 없으며, 불변성을 유지한다.<br />

## 결론 
---
TypeScript의 readonly 속성과 Tuple 타입을 사용하면 데이터의 불변성을 유지하면서도 명확한 타입을 정의할 수 있다.<br />
readonly 속성은 객체나 배열의 요소를 수정할 수 없게 하여 불변성을 보장하고,<br /> 
Tuple 타입은 배열의 특정 위치에 특정 타입의 값이 있어야 함을 보장한다. <br />

이를 통해 더욱 견고하고 유지보수하기 쉬운 코드를 작성할 수 있다.<br />
TypeScript의 강력한 타입 시스템을 활용하여 안전하고 효율적인 코드를 작성해보자.<br />

[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)