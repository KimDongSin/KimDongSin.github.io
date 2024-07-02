---
layout: post
title: isLoading과 isPending차이점
description: isLoading과 isPending차이점을 알아보자.
author: dongsin
date: 2024-06-14 00:10 +09:00
categories: [ReactQuery]
tags: [React, ReactQuery]
pin: false
math: true
mermaid: true
image:
  path:  https://t1.kakaocdn.net/kakao_tech/image/2022/06/images/01.png
---

## React Query에서 isLoading과 isPending 차이점
---
### isLoading
---
* 쿼리가 현재 로딩중이고, 이전에 캐시된 데이터가 없는 상태를 나타낸다.
* 즉, 데이터를 처음으로 가져오는 경우 true가 된다. 
* 사용자에게 첫 로딩 상태를 보여줄 때 유용하다.

### isPending
---
* 쿼리가 현재 데이터를 가져오는 중임을 나타낸다.
* isLoading과 달리, 이전에 캐시된 데이터가 있어도 true가 될 수 있다.
* 즉, 초기 로딩뿐만 아니라 데이터 갱신 시에도 true가 된다.

## 주요 차이점
---
* isLoading은 오직 첫 데이터 로딩 시에만 true이다.
* isPending은 첫 로딩과 이후 데이터 갱신 시에도 true가 될 수 있다.

## 사용 예시
---
* isLoading은 완전히 빈 화면에서 로딩 스피너를 보여줄 때 사용한다.
* isPending은 기존 데이터를 보여주면서 새로운 데이터를 가져오고 있음을 표시할 때 사용한다.

## 결론
---
isLoding과 isPending은 두 상태를 적절히 활용하면 사용자에게 더 나은 로딩 경험을 제공할 수 있다.

