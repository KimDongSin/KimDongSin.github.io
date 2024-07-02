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

## any 타입이란?
---
any 타입은 TypeScript의 타입 시스템에서 "알 수 없음"을 나타내는 타입으로, 어떤 타입의 값이라도 할당할 수 있다.<br />
이는 TypeScript의 엄격한 타입 검사에서 예외가 되는 경우에 사용된다.<br />

any를 사용하게 되면 TypeScript를 사용하는 이유가 없어지게 된다. 주의하자. <br /> 

### any 타입 예시코드
---
```tsx
let value: any;

value = 123; // 숫자 할당
value = "Hello"; // 문자열 할당
value = true; // 불리언 할당

function log(value: any) {
  console.log(value);
}

log(123); // 123
log("Hello"); // Hello
log(true); // true
```
위 예시에서 value 변수는 any 타입으로 선언되어, 숫자, 문자열, 불리언 등 어떤 타입의 값이라도 할당할 수 있다.<br />
또한, log 함수는 any 타입의 인자를 받아 타입 검사를 하지 않고 값을 출력한다.<br />

### any 타입의 장단점
---
any 타입의 장점은 유연성이다. 타입을 명시하지 않거나 다양한 타입을 처리해야 하는 상황에서 유용하다. <br />
그러나 any 타입을 사용하면 TypeScript의 타입 검사 기능을 우회하게 되어<br />
타입 안전성을 보장할 수 없다는 단점이 있다.<br />


## unknown 타입이란?
---
unknown 타입은 TypeScript 3.0에서 도입된 타입으로, "알 수 없음"을 나타내지만 any 타입보다 안전하다.<br />
unknown 타입은 모든 값이 할당될 수 있지만, 실제로 사용하기 위해서는 타입 검사가 필요하다.<br />

```tsx
let value: unknown;

value = 123; // 숫자 할당
value = "Hello"; // 문자열 할당
value = true; // 불리언 할당

function log(value: unknown) {
  if (typeof value === "number") {
    console.log("Number:", value);
  } else if (typeof value === "string") {
    console.log("String:", value);
  } else {
    console.log("Other:", value);
  }
}

log(123); // Number: 123
log("Hello"); // String: Hello
log(true); // Other: true
```

위 예시에서 value 변수는 unknown 타입으로 선언되어, 어떤 타입의 값이라도 할당할 수 있다. <br />
그러나 log 함수에서 value를 사용하기 전에 타입 검사를 통해 안전하게 처리한다.<br />

## unknown 타입의 장단점
unknown 타입의 장점은 타입 안전성을 유지하면서도 유연성을 제공한다는 점이다. <br />
unknown 타입은 값이 실제로 사용되기 전에 타입 검사를 요구하여 타입 안전성을 보장한다.<br />
그러나 사용하기 전에 항상 타입 검사를 해야 하므로 코드가 다소 복잡해질 수 있다.<br />

## any 타입과 unknown 타입 비교
---
| 특징           | `any`   | `unknown` |
| -------------- | ------- | --------- |
| 타입 검사      | 없음    | 필요      |
| 할당 가능한 값 | 모든 값 | 모든 값   |
| 타입 안전성    | 낮음    | 높음      |
| 사용 용이성    | 높음    | 낮음      |

### 사용 비교
---
```tsx
// `any` 타입 사용
function getDataAny(): any {
  return "This is a string";
}

let dataAny = getDataAny();
console.log(dataAny.toUpperCase()); // "THIS IS A STRING"

// `unknown` 타입 사용
function getDataUnknown(): unknown {
  return "This is a string";
}

let dataUnknown = getDataUnknown();

if (typeof dataUnknown === "string") {
  console.log(dataUnknown.toUpperCase()); // "THIS IS A STRING"
} else {
  console.log("Data is not a string");
}
```
위 예시에서 getDataAny 함수는 any 타입을 반환하므로 반환된 값을 타입 검사 없이 바로 사용할 수 있다. <br />
반면, getDataUnknown 함수는 unknown 타입을 반환하므로 값을 사용하기 전에 타입 검사를 해야 한다.<br />

## 결론
---
TypeScript에서 any 타입과 unknown 타입은 각각 다른 목적을 위해 사용된다. <br />
any 타입은 타입 검사를 우회하여 유연하게 값을 처리할 수 있지만, 타입 안전성을 보장하지 않는다.<br />
반면, unknown 타입은 타입 안전성을 유지하면서도 유연성을 제공하여 값이 실제로<br />
사용되기 전에 타입 검사를 요구한다.<br />

[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)