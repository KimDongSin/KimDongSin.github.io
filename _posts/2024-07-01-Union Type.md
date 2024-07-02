---
layout: post
title: Union Type
description: 유니언 타입에 대해 알아보자.
author: dongsin
date: 2024-07-01 12:00 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---

## Union Type이란?
---
Union Types(유니언 타입)은 TypeScript에서 여러 타입 중 하나가 될 수 있는 값을 나타내는 방법이다. <br />
유니언 타입은 `|` 기호를 사용하여 타입들을 결합한다.<br />
이는 변수가 여러 타입의 값 중 하나를 가질 수 있음을 의미한다.<br />

### 유니언 타입의 정의와 사용
---

```tsx
// number 또는 string 타입을 가질 수 있는 변수
let myVar: number | string;

myVar = 10;      // 올바른 사용 예: number 타입
myVar = "Hello"; // 올바른 사용 예: string 타입
myVar = true;    // 오류: boolean 타입은 허용되지 않음
```
위 예제에서 myVar 변수는 number 또는 string 타입 중 하나가 될 수 있다. <br />
따라서 숫자나 문자열을 할당하는 것은 가능하지만, 부울값 등 다른 타입은 할당할 수 없다.<br />

### 유니언 타입을 사용한 함수 매개변수
---
함수 매개변수에서 유니언 타입을 사용할 수 있다. 이는 함수가 여러 타입의 인자를 수용할 수 있게 만든다.<br />
```tsx
// number 또는 string 타입을 받는 함수
function printId(id: number | string) {
    console.log(`ID: ${id}`);
}

printId(100);    // 출력: ID: 100
printId("abc");  // 출력: ID: abc
printId(true);   // 오류: boolean 타입은 허용되지 않음
```

### 유니언 타입을 사용한 객체의 속성
---
객체의 속성으로 유니언 타입을 사용할 수 있다.
이는 해당 속성이 여러 타입 중 하나를 가질 수 있음을 나타낸다

```tsx
// number 또는 string 타입을 가지는 객체
type ID = number | string;

function processId(idInfo: { id: ID, type: string }) {
    console.log(`ID: ${idInfo.id}, Type: ${idInfo.type}`);
}

processId({ id: 100, type: "numeric" });   // 출력: ID: 100, Type: numeric
processId({ id: "abc", type: "string" });  // 출력: ID: abc, Type: string
```

### 유니언 타입의 주의사항
---
유니언 타입을 사용할 때 주의할 점은, 각 타입에 대해 공통적으로 사용할 수 있는 <br />
메서드나 속성만 사용할 수 있다는 점이다.<br />

예를 들어, number와 string의 공통 메서드인 toString()을 사용할 수 있지만,<br />
특정 타입에만 있는 메서드나 속성은 사용할 수 없다.<br />


## Type Alias 대체명 사용하기
---

TypeScript에서는 Type Alias에 대체명(Union)을 사용하여 더 유연하고 복잡한 타입을 정의할 수 있다.<br />
마찬가지로 대체명은 `|` 연산자를 사용하여 여러 타입을 하나로 결합할 수 있다.<br />

```tsx
type ID = number | string;
type Result = Success | Error;

function processResult(result: Result): void {
    if ('message' in result) {
        console.error(`Error: ${result.message}`);
    } else {
        console.log(`Success: ${result.data}`);
    }
}
```

위 예제에서 ID는 number 또는 string 타입을 가질 수 있는 새로운 타입이 되고, <br />
Result는 Success 또는 Error 객체를 가리키는 대체명이다.<br />


## 결론
---
유니언 타입은 TypeScript에서 여러 타입 중 하나가 될 수 있는 값을 표현하는 강력한 도구이다. <br />
이를 통해 코드의 유연성을 높이고, 다양한 상황에서 타입 안정성을 유지할 수 있다.<br />

그러나 사용 시 타입의 규모와 관리를 잘 조정하여야 하며,
필요에 따라 다양한 타입을 적절히 조합하는 것이 중요하다.

[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)