---
layout: post
title: Javascript Static 프로퍼티
categories: javascript
tags: [javascript]
---

[정적 메서드와 정적 프로퍼티](https://ko.javascript.info/static-properties-methods#ref-483)

## 정적 프로퍼티

정적 프로퍼티는 데이터를 클래스 수준에 저장하고 싶을 때 사용한다.<br>

클래스의 다른 인스턴스들과 연결되지 않는다.<br>

일반 클래스 프로퍼티와 유사하나 앞에 `static`이 붙는다.<br>

```javascript
class Article {
  static publisher = "Ilya Kantor";
}

alert(Article.publisher); // Ilya Kantor
```

<br><br>
정적 프로퍼티로 선언하면 클래스 자체에 직접 할당하는 것과 동일하다.<br>

위 예시는 `Article`에 프로퍼티를 직접 할당한 아래 예시와 동일하게 동작한다.<br><br>

```js
Article.publisher = "Ilya Kantor";
```
