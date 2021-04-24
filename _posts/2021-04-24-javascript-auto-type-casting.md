---
title: Javascript 자동 형변환
date: 2021-04-24 17:00:00 +09:00
tags: [javascript]
description: Javascript 자동 형변환


---

## 자바스크립트의 자동 형변환



자바스크립트는 연산자를 사용할 때, 예상되는 데이터 형으로 값을 변환해 연산한다.

```javascript
let a = 3;
let b = "2";

console.log(a-b); // 1
```



`a`는 숫자, `b`는 문자인데 `a-b`의 결과는 `1`이 나온다.

`-` 연산자는 숫자와 숫자를 빼는 경우에만 사용하므로, 숫자 타입이 올 것을 기대하고 있다.

숫자에서 문자를 빼는 것은 `-`  연산자가 할 수 없는 일이므로, b를 숫자로 자동 형변환해 연산을 진행한다.





## 더하기(+) 연산자

```js
number + number // number
number + string // string
string + string // string
string + boolean // string
number + boolean // number

let a = 100;
let b= "점";

console.log(a+b); // 100점

```



- 문자열과 문자열을 concatenate (연결)

- 숫자와 숫자 더하기

- 숫자보다 문자열이 우선

  

`a+b`는 숫자 + 문자열인데, 문자열이 우선되므로 `a`가 string으로 변환되고, 두 문자열이 concatenate 된다.





## 나머지 연산자 (-, *, /, %)

```javascript
string * number // number
string * string // number
number * number // number
string * boolean //number
number * boolean //number

let a = "2";
let b = true;

console.log(a*b); // 2
```

 

더하기 연산을 제외한 다른 연산자는 문자보다 숫자가 우선된다.



`a`는 문자열 "2", `b`는 boolean `true`인데 둘 다 숫자형으로 형변환 되어서 `a*b`는 2이다.



## null과 undefined

```javascript
console.log(1 + null); // 1
console.log("1" + null) // "1null"
console.log(1 - null) // 1
console.log("1" / null) // Infinity
console.log(1 * null) // 0
console.log(1 % null) // NaN
console.log(null + null) // 0
console.log(null + undefined) // NaN

console.log(1 + undefined); // NaN
console.log("1" + undefined); // "1undefined"
console.log(1 - undefined); // NaN
console.log("1" / undefined) // NaN
console.log(1 * undefined) // NaN
console.log(1 % undefined) // NaN
console.log(undefined + undefined) //NaN
```



- null
  - string과 함께 `+` 연산자를 만나면 string으로 형변환
  - 나머지 경우는 number(0)으로 형변환
- undefined
  - string과 함께 `+` 연산자를 만나면 string으로 형변환
  - 나머지 경우는 NaN





## 참조

[자바스크립트의 형변환은 두가지다](https://medium.com/gdana/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98-%ED%98%95%EB%B3%80%ED%99%98%EC%9D%80-%EB%91%90%EA%B0%80%EC%A7%80%EB%8B%A4-b46875be4a88)

[자바스크립트) undefined와 null의 +연산자에 대하여..](https://okky.kr/article/536672)