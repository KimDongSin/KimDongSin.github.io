---
layout: post
title: [TypeScript] type과 interface, 제네릭 사용법
description: TypeScript의 type과 interface, 제네릭의 사용법을 포스팅하였습니다.
author: dongsin
date: 2024-04-21 06:55 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---


# 타입스크립트의 type과 interface, 제네릭 사용법을 알아보자.
>타입스크립트에서는 기본적으로 제공되는 타입말고도 직접 타입을 직접 만들 수 있다.

 1. interface
2. type

크게 2가지 방식이 존재한다.

### type과 interface의 차이점
두가지 방식은 큰 차이는 없지만 사용하는 문법과 메서드가 다르다는 점이 있다.

```ts
export type Restaurant = {
    name:string;
    category:string;
    address:{
        city:string;
        detail:string;
        zipCode:number;
    },
    menu:{
        name:string;
        price:number;
        category:string;
    }[] // menu는 배열이고 안에 객체타입을 지정해주었다.
}
```

## 타입안에 타입만들기
```ts
export type Restaurant = {
    name:string;
    category:string;
    address:Address;
    menu:Menu[];
}

export type Address = {
    city:string;
    detail:string;
    zipCode:number;
}

export type Menu = {
    name:string;
    price:number;
    category:string;
}

```

위의 코드에서 address, menu타입을 타입으로 따로 정의해서 코드를 더 간결하게 뺄 수 있다.


```tsx

let data: Restaurant = {
  name: "식당",
  category: "western",
  address: {
    city: "incheoi",
    detail: "somewhere",
    zipCode: 2321313,
  },
  menu: [
    { name: "rose pasta", price: 2000, category: "PASTA" },
    { name: "garlic steak", price: 3000, category: "aaa" },
  ],
};

const App: React.FC = () => {
  const [myRestaurant, setMyRestaurant] = useState<Restaurant>(data);
  return (
    <div className="App">
      <Store info={myRestaurant} />
    </div>
  );
};
```
useState와 같은 함수에서는 제네릭(<>)문법을 사용하여 타입을 지정해줘야 한다.

useState와 같은 함수에서는 어떠한 타입이 들어갈지 상황마다 달라지기 때문에 제네릭으로 적용 시켜줘야 한다.


## interface로 타입 정의
위의 코드에서 type을 정의하고, 제네릭을 사용하여 useState의 타입도 지정해주었는데

tsx부분의 Store에서 에러가 사라지지않았다.

그 이유는 props의 타입을 지정해주지 않아서 에러를 발생시키는 것이다.

보통 props의 경우 props의 타입을 따로 만들어준다.

interface를 사용하여 store props타입을 지정해주겠다.

```tsx
// store.tsx

import React from "react";
import { Restaurant } from "./model/resturant";

interface OwnProps {
  info: Restaurant;
}

const Store: React.FC<OwnProps> = ({info) => {
  return <div>Store</div>;
};

export default Store;

```

위와 같이 interface로 props의 타입을 지정해주고, React:FC에서는 제네릭으로 타입을 지정해준다.

그리고 App.tsx를 확인해보면 Store의 에러가 사라진 것을 확인 할 수 있다.

## 함수 타입스크립트로 정의하는 방법
address를 변경하는 함수를 만들어보자.

```tsx
// App.tsx

import React, { useState } from "react";
import "./App.css";
import Store from "./Store";
import { Address, Restaurant } from "./model/resturant";

let data: Restaurant = {
  name: "식당",
  category: "western",
  address: {
    city: "incheoi",
    detail: "somewhere",
    zipCode: 2321313,
  },
  menu: [
    { name: "rose pasta", price: 2000, category: "PASTA" },
    { name: "garlic steak", price: 3000, category: "aaa" },
  ],
};

const App: React.FC = () => {
  const [myRestaurant, setMyRestaurant] = useState(data);
  const changeAddress = (address: Address) => { // 따로 뺀 Address를 가져옴.
    setMyRestaurant({ ...myRestaurant, address: address });
  };
  return (
    <div className="App">
      <Store info={myRestaurant} changeAddress={changeAddress} />
    </div>
  );
};

export default App;

```

그리고 Store에서도 changeAddress props의 타입을 지정해줘야한다.

```tsx
// Store.tsx

import React from "react";
import { Address, Restaurant } from "./model/resturant";

interface OwnProps {
  info: Restaurant;
  changeAddress(address: Address): void; // type이 없을 땐 void
  //Ex -> 만약 return타입이 true가 온다면 boolean타입을 쓴다.
}

const Store: React.FC<OwnProps> = ({ info }) => {
  console.log(info);

  return <div>Store</div>;
};

export default Store;

```



[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)