---
title: JavaScript ES6 Generator
date: 2021-04-14 21:51:00 +09:00
tags: [javascript]
category: [posts]
description: JavaScript ES6의 Generator에 대해 알아봅시다.
---

# 제너레이터

일반 함수는 하나의 값(혹은 0개)만을 반환한다.

제너레이터는 여러 개의 값을 하나씩 반환(yield)할 수 있다.

## 제너레이터 함수

제너레이터를 만들기 위해서는 `function*` 이라는 특별한 문법 구조를 사용해야함.

```javascript
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}

// 제너레이터 함수는 제너레이터 객체를 생성한다.
let generator = generateSequence();
alert(generator); // [object Generator]
```

이 때 함수 본문 코드는 실행되지 않은 상태!

`next()`를 호출하면 `yield`문을 만날 떄까지 실행이 지속됨.

`yield`문을 만나면 실행이 멈추고 그 코드에서 산출된 값이 바깥 코드에 반환됨.

`next()`는 다음과 같은 두 프로퍼티를 가진 객체를 반환한다.

- `value`: 산출값

- `done`: 함수 실행 끝났으면 `true`, 아니면 `false`

```javascript
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}

let generator = generateSequence();

let one = generator.next();

alert(JSON.stringify(one)); // {value: 1, done: false}
```
