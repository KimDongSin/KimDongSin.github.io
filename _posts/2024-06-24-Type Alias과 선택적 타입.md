---
layout: post
title: Type Alias과 선택적 타입
description: Type Alias과 선택적 타입
author: dongsin
date: 2024-06-24 12:00 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---

## TypeScript의 Type  Alias와 선택적 타입
TypeScript는 JavaScript에 타입 시스템을 추가하여 코드를 더 안전하고 유지보수하기 쉽게 만들어준다.

### Type Alias란?
---
Type Alias(타입 별칭)는 특정 타입에 이름을 부여하여 코드의 가독성을 높이고 재사용성을 향상시키는 기능이다.<br /> 인터페이스와 유사하지만, 더 다양한 타입 정의가 가능하다.<br />

### Type Alias 예시코드
---
```tsx
type User = {
  id: number;
  name: string;
  email: string;
};

// User 타입을 사용한 함수
const getUser = (user: User): string => {
  return `User Name: ${user.name}, Email: ${user.email}`;
};

const user: User = { id: 1, name: 'John Doe', email: 'john@example.com' };
console.log(getUser(user));
```
위 예시에서 User 타입 별칭을 정의하여 객체의 구조를 명확하게 하고, 여러 곳에서 재사용할 수 있다.<br />


### 선택적 타입(Optional Types)
---
TypeScript에서는 객체의 속성이 선택적(Optional)일 수 있다. <br />
선택적 속성은 존재할 수도, 존재하지 않을 수도 있으며, 이를 정의하기 위해 속성 이름 뒤에 물음표(?)를 붙인다.<br />

### 선택적 타입 예시코드
---
```tsx
type User = {
  id: number;
  name: string;
  email?: string; // 선택적 속성
};

const getUserInfo = (user: User): string => {
  return `User Name: ${user.name}, Email: ${user.email ? user.email : 'No Email'}`;
};

const user1: User = { id: 1, name: 'John Doe' }; // email 속성 없음
const user2: User = { id: 2, name: 'Jane Doe', email: 'jane@example.com' };

console.log(getUserInfo(user1)); // User Name: John Doe, Email: No Email
console.log(getUserInfo(user2)); // User Name: Jane Doe, Email: jane@example.com
```
위 예시에서 email 속성은 선택적 속성으로 정의되었다.<br />
user1 객체에는 email 속성이 없고, user2 객체에는 email 속성이 있다.<br />
선택적 속성을 통해 객체의 유연성을 높일 수 있다.<br />

### Type Alias와 선택적 타입의 활용
---
Type Alias와 선택적 타입을 함께 사용하면 더욱 강력한 타입 시스템을 구축할 수 있다.

```tsx
type Address = {
  street: string;
  city: string;
  postalCode: string;
  country?: string; // 선택적 속성
};

type User = {
  id: number;
  name: string;
  email?: string;
  address: Address; // 중첩된 Type Alias
};

const getUserDetails = (user: User): string => {
  const { name, email, address } = user;
  const country = address.country ? `, Country: ${address.country}` : '';
  return `User Name: ${name}, Email: ${email ? email : 'No Email'}, Address: ${address.street}, ${address.city}, ${address.postalCode}${country}`;
};

const user: User = {
  id: 1,
  name: 'John Doe',
  address: { street: '123 Main St', city: 'Anytown', postalCode: '12345' }
};

console.log(getUserDetails(user));
// User Name: John Doe, Email: No Email, Address: 123 Main St, Anytown, 12345
```
이 예시에서는 User 타입과 Address 타입을 별칭으로 정의하고, 선택적 속성을 사용하여<br />
더욱 유연한 객체를 만들었다. 이를 통해 타입 정의가 명확해지고, 코드의 가독성과 유지보수성이 향상된다.<br />

## 결론
---
TypeScript의 Type Alias와 선택적 타입은 코드를 더 명확하고 유지보수하기 쉽게 만들어주는 강력한 도구이다. <br />
Type Alias를 통해 타입 정의를 재사용하고, 선택적 타입을 통해 객체의 유연성을 높일 수 있다.<br />
이를 활용하여 TypeScript 프로젝트에서 안전하고 효율적인 코드를 작성해보자.<br />

[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)