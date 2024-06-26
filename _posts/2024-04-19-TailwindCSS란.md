---
layout: post
title: TailwindCSS를 알아보자
description: TailwindCSS에 장/단점 사용 이유에 대해 포스팅하였습니다.
author: dongsin
date: 2024-04-19 23:59:00 +09:00
categories: [TailwindCSS]
tags: [TailwindCSS]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/js43o/post/3ab8d087-c4f4-46b5-8f65-6d5e1736b58e/image.png
  alt: Tailwind 이미지
---



# Tailwind란?
<!-- h1 -->

> 테일윈드(Tailwind)는 CSS 프레임워크로, HTML 요소에 직접 클래스를 적용하여 스타일을 적용하는 방식이다. <br />
이를 통해 개발자는 기존의 CSS 작업 방식과는 다르게 클래스 기반의 스타일링을 통해 유연한 디자인을 구현할 수 있으며, 테일윈드는 사전에 정의된 수많은 클래스를 제공하여 필요한 스타일을 쉽고 빠르게 적용할 수 있다.


## Tailwind 장점
 1. 유연한 디자인: 테일윈드는 클래스 기반의 스타일링을 통해 매우 유연한 디자인이 가능하며, 이는 개발자가 필요한 스타일을 직접 정의할 수 있어서 디자인에 큰 제약을 받지 않고 작업할 수 있게 한다.

2. 성능: 테일윈드는 CSS를 미리 정의해놓고 클래스로 조합하는 방식을 채택하여, 성능 측면에서도 우수하다. 
<br />불필요한 CSS를 생성하지 않고, 필요한 스타일만 적용되기 때문에 페이지 로딩 속도를 향상시킬 수 있다.

3. 커스터마이징 용이성: 테일윈드는 각 클래스에 대해 커스텀할 수 있는 많은 옵션을 제공한다.<br /> 이를 통해 개발자는 디자인 요소를 쉽게 수정하거나 추가할 수 있다.

 4. 반응형 디자인: 테일윈드는 반응형 디자인을 쉽게 구현할 수 있도록 도와준다.<br /> 사전 정의된 반응형 클래스를 사용하여 레이아웃을 조정하고, 장치의 크기에 따라 스타일을 변경할 수 있다.

## Tailwind 단점
러닝 커브: 테일윈드를 처음 사용하는 개발자에게는 학습 곡선이 존재할 수 있고, 기존의 CSS와는 다른 접근 방식이기 때문에 익숙해지는 데에 시간이 필요할 수 있다.

파일 크기: 테일윈드를 사용하면 HTML 파일이 더 커질 수 있다. 이는 클래스 기반의 스타일링을 사용하기 때문에 추가 클래스가 필요하고, 이로 인해 파일 크기가 증가할 수 있다.

## 사용하는 이유

속도와 생산성 향상: 테일윈드는 빠르고 효율적인 개발을 돕는다. 사전 정의된 클래스를 사용하여 스타일을 빠르게 적용할 수 있으며, 이는 개발 시간을 단축시키고 생산성을 향상시킨다.

 유지보수 용이성: 테일윈드를 사용하면 스타일을 중앙 집중화할 수 있다. 이는 코드의 가독성을 향상시키고 유지보수를 더욱 쉽게 만든다.

 커스터마이징 가능성: 테일윈드는 매우 유연하게 커스터마이징할 수 있다. 필요에 따라 커스텀 클래스를 추가하거나 수정하여 디자인을 자유롭게 조절할 수 있다.


## 사용법

### 1. 설치
프로젝트에 테일윈드를 설치하며, 이는 npm을 통해 설치할 수 있다.
> npm i tailwindcss


### 적용방법

```tsx
<body>
    <div class="bg-gray-200 p-4">
        <h1 class="text-2xl font-bold text-center text-blue-600">제목</h1>
        <p class="text-lg text-gray-800 mt-4">설명</p>
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mt-4">버튼</button>
    </div>
</body>
```

이후 HTML, JSX, TSX 등의 파일에서 필요한 요소에 테일윈드 클래스를 적용한다.<br />
테일윈드에서 적용되는 CSS속성을 모를 경우 공식문서에 검색해보면 쉽게 찾을 수 있다.


### 2. 커스텀화

필요에 따라 테일윈드의 클래스를 커스텀하여 스타일을 조절한다.<br />tailwind.config.js 파일을 통해 커스텀 테마나 클래스를 정의할 수 있다.

```js
// tailwind.config.js

module.exports = {
  purge: [],
  darkMode: false, // 또는 'media' 또는 'class'
  theme: {
    extend: {
      colors: {
        // 사용자 정의 색상 추가
        primary: '#FF6347',
        secondary: '#1E90FF',
      },
      fontFamily: {
        // 사용자 정의 폰트 추가
        'custom': ['Nunito', 'sans-serif'],
      },
      spacing: {
        // 사용자 정의 여백 추가
        '72': '18rem',
        '84': '21rem',
      },
    },
  },
  variants: {
    extend: {},
  },
  plugins: [],
}

```


 예를 들어, .bg-primary 클래스를 사용하여 기본색상이 아닌 사용자 정의된 primary 색상을 적용할 수 있다.<br /> 마찬가지로 .font-custom 클래스를 사용하여 Nunito 폰트를 적용할 수 있다.

***

## 결론
테일윈드는 CSS를 쉽고 효율적으로 작업할 수 있게 해주는 강력한 도구이다. 그러나 사용하기 전에 장단점을 고려하여 프로젝트의 요구 사항에 맞게 선택하는 것이 중요하다.

[Tailwind 공식문서](https://tailwindcss.com/docs/installation)