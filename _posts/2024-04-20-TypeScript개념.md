---
layout: post
title: TypeScript기본개념과 사용법
description: TypeScript의 개념과 간단 사용법을 정리하였습니다.
author: dongsin
date: 2024-04-20 12:00 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---


# 타입스크립트란?
> 타입스크립트는 자바스크립트에 타입을 부여한 언어이다.<br />
자바스크립트의 확장된 언어라고 볼 수 있다.

## TypeScript의 장점
> TypeScript를 사용하는 가장 큰 목적은 정적타입을 지원한다는 것이다.


## 타입 지정방법

```ts
let a: number = 123;

a = 123;
```

a변수의 타입을 number로 지정하였다.
이렇게 되면 a변수에는 number타입 외에 다른 타입을 넣게 되면 에러를 발생시킨다.

만약 타입을 여러개 지정하고 싶다면 | 연산자로 타입을 여러개 지정해 줄 수 있다.

```ts
let a: number | string = 123;

a = "문자입니다.";
```

위와 같이 number 또는 string 타입만 받게 할 수 있다.<br />

```ts
let a:any = 123;

a = "null"; // null
a = "문자"; // "문자"
a = 435; // 435

```

만약 타입이 어떤게 들어올 지 모른다면 any타입으로도 지정해 줄 수 있으나,<br />any타입을 쓴다면
ts를 쓰는 이유가 사라지게 된다. <br />

따라서 상황에 맞게 사용하되 any타입의 사용을 최대한 지양해야 된다.

### 배열 타입지정

```ts
let numArr: number[] = [1, 2, 3];

numArr.push(4);
numArr.push("a"); // 문자열을 넣어서 에러가 발생한다.

```

배열의 타입도 코드와 같이 지정해 줄수 있으며, 위와 마찬가지로 타입이 어긋나면 에러를 발생시킨다.


### 함수 타입지정
```ts
function addNumber(a:number, b:number):number{
    return a+b;
}

addNumber(5, 5);
```

함수도 마찬가지로 타입을 지정할 수 있다.
파라미터 a, b number타입으로 지정하였고 함수에도 number타입으로 return되게 설정하였다.

addNumber에 number type 5, 5를 넣으면 number type의 10이 반환되는 것을 확인 할 수 있다.

## tsc
> tsc index.ts
명령어를 사용하면 ts의 파일을 자동으로 js로 변환하여 실행시켜준다.


## tsconfig설정
다음과 같이 tsconfig파일에서 es5 혹은 es6로 반환받을 지부터 이외 설정을 설정해 줄 수 있다.
```
{
 "compilerOptions": {

  "target": "es5", // 'es3', 'es5', 'es2015', 'es2016', 'es2017','es2018', 'esnext' 가능
  "module": "commonjs", //무슨 import 문법 쓸건지 'commonjs', 'amd', 'es2015', 'esnext'
  "allowJs": true, // js 파일들 ts에서 import해서 쓸 수 있는지 
  "checkJs": true, // 일반 js 파일에서도 에러체크 여부 
  "jsx": "preserve", // tsx 파일을 jsx로 어떻게 컴파일할 것인지 'preserve', 'react-native', 'react'
  "declaration": true, //컴파일시 .d.ts 파일도 자동으로 함께생성 (현재쓰는 모든 타입이 정의된 파일)
  "outFile": "./", //모든 ts파일을 js파일 하나로 컴파일해줌 (module이 none, amd, system일 때만 가능)
  "outDir": "./", //js파일 아웃풋 경로바꾸기
  "rootDir": "./", //루트경로 바꾸기 (js 파일 아웃풋 경로에 영향줌)
  "removeComments": true, //컴파일시 주석제거 

  "strict": true, //strict 관련, noimplicit 어쩌구 관련 모드 전부 켜기
  "noImplicitAny": true, //any타입 금지 여부
  "strictNullChecks": true, //null, undefined 타입에 이상한 짓 할시 에러내기 
  "strictFunctionTypes": true, //함수파라미터 타입체크 강하게 
  "strictPropertyInitialization": true, //class constructor 작성시 타입체크 강하게
  "noImplicitThis": true, //this 키워드가 any 타입일 경우 에러내기
  "alwaysStrict": true, //자바스크립트 "use strict" 모드 켜기

  "noUnusedLocals": true, //쓰지않는 지역변수 있으면 에러내기
  "noUnusedParameters": true, //쓰지않는 파라미터 있으면 에러내기
  "noImplicitReturns": true, //함수에서 return 빼먹으면 에러내기 
  "noFallthroughCasesInSwitch": true, //switch문 이상하면 에러내기 
 }
}
```

