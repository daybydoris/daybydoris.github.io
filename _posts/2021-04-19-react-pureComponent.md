---
title: React.PureComponent란?
date: 2021-04-19 21:40:00 +09:00
tags: [react]
category: [posts]
description: React.PureComponent에 대해 알아봅시다.
---

`React.PureComponent`는 `React.Component`와 비슷하다.

`React.Component`는 `shouldComponentUpdate()`를 구현하지 않지만, `React.PureComponent`는 props와 state를 이용한 **얕은 비교**를 구현한다는 차이점이 있다.

## 얕은 비교(shallow compare)

- equality를 체크하는 것
- 숫자가 문자열 같은 scalar 값들을 비교할 때는 **값**을 비교함
- 단, **object**를 비교할 때는 attribute가 아니라 **reference를 비교**함
  - 레퍼런스만 체크하기 때문에 같은 값이 들어있는 object라도 항상 다른값으로 체크하게 됨.

## React.PureComponent

- pureComponent는 shouldComponentUpdate가 이미 적용된 버전의 React.Component이다
- pureComponent는 renderer에서 shouldComponentUpdate를 수행할 때 **shallow compare**를 수행함
- 불필요한 state 변화 감지로 인한 **재렌더링을 줄임**으로써 성능 극대화

## React.PureComponent를 사용할 수 있는 상황

- state와 props이 **immutable**일 때
  - state과 props가 변하지 않음에도 object라서 reference로 다름을 체크해 항상 다르다고 판단되기 때문에
- state와 props이 hierarchy 혹은 복잡한 구조를 가지고 있을 때
- sholudComponentUpdate lifecycle을 사용하지 않을 계획일 때

[React 최상위 API - React](https://ko.reactjs.org/docs/react-api.html#reactpurecomponent)
