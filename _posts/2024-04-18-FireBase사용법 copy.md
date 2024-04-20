---
layout: post
title: 파이어베이스(FireBase) 사용법
description: 파이어베이스(FireBase)의 사용법을 간단정리하였습니다.
author: dongsin
date: 2024-04-18 23:59:00 +09:00
categories: [FireBase]
tags: [파이어베이스, FireBase]
pin: false
math: true
mermaid: true
image:
  path: https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99F03A335A026DE21E
  alt: 파이어베이스 이미지
---


# 파이어베이스의 Firestore 사용법
<!-- h1 -->

> 파이어베이스 Firestore는 실시간 데이터베이스로, 클라우드 기반의 NoSQL 문서형 데이터베이스다. Firestore를 사용하면 앱 데이터를 쉽게 저장, 동기화 및 쿼리할 수 있다.


## Firestore 설정
먼저, Firestore를 사용하려면 Firebase 프로젝트에 Firestore를 활성화해야 한다. Firebase 콘솔에서 프로젝트를 선택하고 'Firestore 데이터베이스' 섹션으로 이동하여 설정할 수 있다.

## Firestore 데이터 모델링
Firestore는 컬렉션(Collection)과 문서(Document)라는 두 가지 주요 데이터 구조를 사용한다. 컬렉션은 문서의 그룹이고, 문서는 필드와 해당 필드의 값으로 이루어진 데이터이다.

예를 들어, 사용자 컬렉션에는 각 사용자에 대한 문서가 있을 수 있다. 각 문서는 사용자의 이름, 이메일, 프로필 사진 URL 등과 같은 필드를 포함할 수 있다.

## Firestore 데이터 추가
Firestore에서 데이터를 추가하는 것은 간단하다.<br />
사용자 컬렉션에 새로운 사용자를 추가를 한다고 가정해보자.
```js
// Firestore 인스턴스 가져오기
const db = firebase.firestore();

// 사용자 데이터 추가
db.collection("users").add({
    name: "John Doe",
    email: "johndoe@example.com",
    age: 30
})
.then((docRef) => {
    console.log("Document written with ID: ", docRef.id);
})
.catch((error) => {
    console.error("Error adding document: ", error);
});

```

위와 같이 db.collection함수로 데이터를 간단하게 추가할 수 있다.


## Firestore 데이터 조회
```js
// 사용자 컬렉션에서 모든 사용자 가져오기
db.collection("users").get().then((querySnapshot) => {
    querySnapshot.forEach((doc) => {
        console.log(`${doc.id} => ${doc.data()}`);
    });
})
.catch((error) => {
    console.log("Error getting documents: ", error);
});

```

모든 사용자를 가져오는 코드이다.

## Firestore 실시간 업데이트
```js
// 사용자 컬렉션에서 실시간 업데이트 수신하기
db.collection("users").onSnapshot((querySnapshot) => {
    querySnapshot.forEach((doc) => {
        console.log(`${doc.id} => ${doc.data()}`);
    });
});

```

Firestore는 실시간 업데이트를 제공하여, 데이터베이스의 변경 사항을 즉시 반영할 수 있다.

***
### 결론
> 파이어 베이스 Firestore는 강력한 클라우드 기반 데이터베이스로, 앱의 데이터관리를 간편하게 해준다.
