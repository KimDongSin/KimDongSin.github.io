---
layout: post
title: type, interface extends하는 방법
description: TypeScript의 type, interface에 extends하는 방법을 알아보자.
author: dongsin
date: 2024-04-22 01:20 +09:00
categories: [TypeScript]
tags: [TypeScript]
pin: false
math: true
mermaid: true
image:
  path: https://velog.velcdn.com/images/lsx2003/post/24521b5c-d1a8-4df3-9fed-43b26788a005/image.png
  alt: TypeScript 이미지
---

## interface extends란?

interface를 extends로 상속시켜 줄 수 있다.

BestMenu컴포넌트를 생성하고, App컴포넌트에서 BestMenu에 props를 전달해보겠다.

```tsx
// App.tsx

const App: React.FC = () => {
  const [myRestaurant, setMyRestaurant] = useState(data);
  const changeAddress = (address: Address) => {
    setMyRestaurant({ ...myRestaurant, address: address });
  };

  return (
    <div className="App">
      <Store info={myRestaurant} changeAddress={changeAddress} />
      <BestMenu
        name="불고기피자"
        category="피자"
        price={1000}

      />
    </div>
  );
};
```

그리고 BestMenu컴포넌트에서 props를 읽어오겠다.

```tsx
// BestMenu.tsx

import React from "react";

interface OwnProps extends Menu {
  name:string,
  category:string,
  price:number
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

위와 같이 OwnProps에 타입을 지정해주면 되는데,

이미 따로 타입을 지정해준 ts파일에서 type을 extends로 상속해주면 저렇게 일일히

해줄 필요없이 간편하게 코드를 짤 수 있다.

```tsx
import React from "react";
import { Menu } from "./model/resturant";

interface OwnProps extends Menu {
  showBestMenuName(name: string): string;
}

const BestMenu: React.FC<OwnProps> = ({
  name,
  price,
  category,
}) => {
  return <div>BestMenu</div>;
};

export default BestMenu;

```

위의 코드와 같이 OwnProps에 Menu타입을 extends로 상속시켜서 타입을 지정하였다.

그리고 App컴포넌트에서 추가적으로 베스트메뉴를 보여주는 함수를 추가로 만들어보겠다.

```tsx
// App.tsx

import React, { useState } from "react";
import "./App.css";
import Store from "./Store";
import { Address, Restaurant } from "./model/resturant";
import BestMenu from "./BestMenu";

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
        price={1000}
        showBestMenuName={showBestMenuName}
      />
    </div>
  );
};

export default App;

```

```tsx
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
그리고 OwnProps에 showBestMenuName의 타입을 지정해주면 끝이다.


## type으로 상속 하는 방법

```tsx
import React from "react";
import { Menu } from "./model/resturant";

type OwnProps = Menu & {
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

---
## 결론

extends를 잘 활용하면 미리 만든 타입을 상속으로 받아오기때문에<br />
하드코딩으로 인한 실수도 방지할 수 있고, 코드의 양을 확 줄일 수 있다는 장점이 있다.





[TypeScript 공식문서](https://yamoo9.gitbook.io/typescript)