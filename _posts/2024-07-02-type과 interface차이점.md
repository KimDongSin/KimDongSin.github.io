---
layout: post
title: Type Alias와 interface차이점
description: TypeScript에서의 객체 표현 방식
author: dongsin
date: 2024-07-02 12:00 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---

## TypeScript에서의 객체 표현 방식
---
TypeScript에서 객체를 정의하는 주요 방법은 두 가지가 있다 => `Type Alias`와 `interface`이다. <br />

## 방식 비교
---
### Type Alias 방식
```tsx
type PlayerType = {
    nickname: string,
    team: TeamType,
    health: HealthType
};
```

### interface 방식
```tsx
interface PlayerInterface {
    nickname: string,
    team: TeamType,
    health: HealthType
}
```

## type과 interface의 차이점
---
### 사용 범위의 차이
type 키워드는 다양한 타입 정의에 유리하며, 유니온 타입, 튜플 등을 포함한 <br />
다양한 형태로 타입을 정의할 수 있다.<br />
 
반면 interface는 주로 객체의 구조를 정의하는 데 사용됩니다.<br />
 
### 타입 축적 기능
interface는 같은 이름의 여러 선언을 합쳐 하나의 인터페이스로 결합할 수 있어, <br />
객체의 구조를 확장하거나 세분화하는 데 유용하다.<br />

예를 들어, 다음과 같이 여러 인터페이스를 하나의 객체 타입으로 정의할 수 있다.<br />

```tsx
interface UserInterface {
    name: string;
}

interface UserInterface {
    lastName: string;
}

interface UserInterface {
    health: number;
}

const user: UserInterface = {
    name: "John",
    lastName: "Doe",
    health: 100
};
```
이러한 기능은 type에서는 지원되지 않는다.

## 결론
---
* type과 interface는 각각 다양한 용도로 사용될 수 있으며, 객체를 특정 형태로 정의하는 방법에<br />따라 선택하여 사용하면 된다.
* 객체의 구조를 세밀하게 정의하거나 확장해야 할 경우에는 interface가 유용하며, 
<br />다양한 타입을 포괄하는 정의가 필요할 때는 type을 사용하는 것이 적합하다.

[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)