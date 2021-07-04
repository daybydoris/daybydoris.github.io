---
title: JavaScript ES6 비구조화 할당 문법
date: 2021-04-14 21:10:00 +09:00
tags: [javascript]
category: [posts]
description: JavaScript ES6의 비구조화 할당 문법에 대해 알아봅시다.
---

# 비구조화 할당 문법

객체 안에 있는 값을 추출해 변수 혹은 상수로 바로 선언하는 문법

## 객체 비구조화 할당

```javascript
const object = { a: 1, b: 2 };

const { a, b } = object;

console.log(a); // 1
console.log(b); // 2
```

## 함수의 파라미터에서 비구조화 할당 사용

```javascript
const object = { a: 1, b: 2 };

function print({ a, b }) {
  console.log(a);
  console.log(b);
}

print(object); // 파라미터로 전달된 객체가 a, b로 할당된다.
```

## 비구조화 할당 시 기본값 설정

특정 값이 주어지지 않을 경우 기본값을 설정해줄 수 있다.

```javascript
const object = { a: 1 };

function print({ a, b = 2 }) {
  // object 객체에 b는 없지만 b = 2로 기본값이 설정됨
  console.log(a);
  console.log(b);
}

print(object);
// 1
// 2
```

## 깊은 값 비구조화 할당

- 방법 1 : 비구조화 할당 여러번 하기

```javascript
const deepObject = {
  state: {
    information: {
      name: "velopert",
      languages: ["korean", "english", "chinese"],
    },
  },
  value: 5,
};

const { name, languages } = deepObjects.state.information;
const { valule } = deepObject;

const extracted = {
  name,
  languages,
  value,
};

console.log(extracted); // {name: "velopert", languages: Array[3], value: 5}
```

- 방법 2 : 비구조화 할당 한번에 하기

  ```javascript
  const deepObject = {
    state: {
      information: {
        name: "velopert",
        languages: ["korean", "english", "chinese"],
      },
    },
    value: 5,
  };

  const {
    state: {
      information: { name, languages },
    },
    value,
  } = deepObject;

  const extracted = {
    name,
    languages,
    value,
  };

  console.log(extracted); // {name: "velopert", languages: Array[3], value: 5}
  ```

참조 : https://learnjs.vlpt.us/useful/06-destructuring.html
