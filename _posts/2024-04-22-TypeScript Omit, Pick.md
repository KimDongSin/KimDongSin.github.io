---
layout: post
title: Omit과 Pick사용법
description: TypeScript의 Omit과 Pick사용법을 포스팅하였습니다.
author: dongsin
date: 2024-04-22 14:47 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---


## Omit이란?
정의되어 있는 타입에서 특정 속성만 빼고 싶을 때 사용한다.

### Omit사용법

```ts
export type Address = {
    city:string;
    detail:string;
    zipCode:number;
}

// 이렇게 하지않고도 Omit으로 해결할 수 있다.
export type newAddress = {
    city:string;
    detail:string;
}
```
예를 들어 Address type에서 정의된 값들 중 zipCode만 빼주고 싶다면<br />
newAddress와 같이 할 수도 있지만 Omit을 사용하여 간편하게 해결할 수 있다.

```ts
export type AddressWithoutZip = omit <Address, 'zipCode'>
```
위와 같이 Omit을 사용하면 newAddress와 같이 zipCode값만 제외한 나머지 값이 할당된다.



## Omit 적용

```tsx
// App.tsx
const App: React.FC = () => {
  const [myRestaurant, setMyRestaurant] = useState(data);
  const changeAddress = (address: Address) => {
    setMyRestaurant({ ...myRestaurant, address: address });
  };

  const showBestMenuName = (name: string) => {
    return name;
  };
  return (
    <div className="App">
      <Store info={myRestaurant} changeAddress={changeAddress} />
      <BestMenu
        name="불고기피자"
        category="피자"
        showBestMenuName={showBestMenuName}
      />
    </div>
  );
};


// BestMenu.tsx

import React from "react";
import { Menu } from "./model/resturant";

interface OwnProps extends Menu {
  showBestMenuName(name: string): string;
}

const BestMenu: React.FC<OwnProps> = ({
  name,
  price,
  category,
  showBestMenuName,
}) => {
  return <div>BestMenu</div>;
};

export default BestMenu;

```

App.tsx에서 price를 빼면 BestMenu에서는 price를 타입으로 정의하고 있기때문에<br />
타입은 반드시 받아야하므로 에러가 발생한다.

이때 Omit을 사용하면 간단하게 해결할 수 있다.

```tsx
import React from "react";
import { Menu } from "./model/resturant";

interface OwnProps extends Omit<Menu, 'price'> {
  showBestMenuName(name: string): string;
}

const BestMenu: React.FC<OwnProps> = ({
  name,
  category,
  showBestMenuName,
}) => {
  return <div>BestMenu</div>;
};

export default BestMenu;

```

그리고 여러개의 타입을 제거할 때  ‘ | ’ 를 사용하여 다수의 타입을 제거할 수있다.
```ts
interface OwnProps extends Omit<Menu, 'price' | 'name'> {
  showBestMenuName(name: string): string;
}
```
결과적으로 price와 name속성을 제외한 나머지 속성형태를 가지게 된다.


## Pick이란?
Pick은 다른 타입에서 몇개의 속성만을 선택하여 새로운 타입을 만드는데 사용한다.

```ts
export type RestaurantOnlyCategory = Pick<Restaurant, 'category'>
```
RestaurantOnlyCategory타입은 Restaurant타입에서 category 속성만을 가지게 된다.

## es6+ 문법을 사용하여 Omit대체하기
```ts
export type Address = {
    city:string;
    detail:string;
    zipCode?:number;
}
```
? 문법으로 zipCode가 있을수도 있고 없을수도 있다로 처리할 수 있다.<br />
다만 반드시 zipCode속성이 있어야할 때는 주의해서 사용해야한다.


## 결론
Omit은 특정 속성만 제거한 나머지의 타입형태를 가지게 된다.

Pick은 Omit과 반대로 특정 타입의 속성만을 가지게 된다.

es6+ 문법인 ?로 Omit을 대체할 수 있지만 필수 속성으로 들어와야할 때는 지양한다.



[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)