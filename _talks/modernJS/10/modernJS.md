---
title: "[모던 자바 스크립트] 10장 객체 리터럴"
collection: talks
type: "Talk"
permalink: _talks/modernJS/11/modernJS
date: 2024-03-10
---

# 10. 객체 리터럴

---

자바스크립트는 객체기반의 프로그래밍 언이이며 이를 구성하는 거의 모든것이 객체

원시값은 변경불가능하지만 객체타입은 변경 가능하다.

객체는 프로퍼티와 메서드로 구성된 집합체이다.

- 프로퍼티 : 객체의 상태를 나타내는 값
- 메서드 : 프로퍼티(상태 데이터)를 참조하고 조작할수 있는 동작

### 객체와 함수

자바스크립트에서는 함수로 객체를 생성하기도 하며 함수 자체가 객체이다

### 인스턴스

클래스에 의해 생성되어 메모리에 저장된 실체 <br>
객체지향 프로그래밍에서 객체는 클래스와 인스턴스를 포함한 개념이다. <br>
클래스는 인스턴스를 생성하기 위한 템플릿의 역할을 수행한다.

### 객체 리터럴에 의한 객체 생성

리터럴: 사람이 이해할수 있는문자또는 약속된 기호를 사용하여 값을생성하는 표기법
객체 리터를 은 중괄호 ({...})내에 0개 이상의 프로퍼티를 정의한다

```javascript
var person = {
  name: "minjun",
  sayhi: function () {
    console.log(`hello ${this.name}`);
  },
};

console.log(person); // {name: 'minjun' , sayhi: f}
```

### 프로퍼티

<b>객체는 프로퍼티의 집합이며, 프로퍼티는 키와 값으로 구성된다</b>

```javascript
var person = {
  name: "minjun", // key : name , value : 'minjun'
  age: "27",
};
```

- 프로퍼티 key : 빈 문자열을 포함하는 모든 문자열 또는 심벌값
- 프로퍼티 값 : 자바스크립트에서 사용할수 있는 모든값

프로퍼티 key 동적 생성

```javascript
var obj = {};
var key = "hi";

obj[key] = "hihi";

console.log(obj); // {hi:hihi}
```

### 메서드

프로퍼티 값이 함수일 경우 일반함수와 구분을 위해 매서드라 부른다<br>
객체에 묶여 있는 함수를 메서드라 칭한다

### 프로퍼티 접근

- 마침표 표기법 (.) 사용
- 접근 연산자 [...]사용

```javascript
console.log(person.name);
console.log(person["name"]); //접근연산자 사용시 따옴표 필수
```

### 프로퍼티 생성

```javascript
person.age = 20; // {age: 20}
```

### 프로퍼티 삭제

```javascript
delete person.age; // age 프로퍼티 삭제
```

### 프로퍼티 축약 (es6 추가)

변수를 사용하는경우 변수이름과 프로퍼티키가 동일하는 경우 생략 가능

```javascript
let x = 1,
  y = 2;
const obj = { x, y };
console.log(obj); // {x :1, y:2}
```

### 계산된 프로퍼티 이름 (es6 추가)

객체 리터럴 내부에서 계산된 프로퍼티이름으로 프로퍼티 키 동적생성

```javascript
const prefix = "prop";
let i = 0;
const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
};

console.log(obj); // {prop-1 :1, prop-2 :2, prop-3 :3,}
```

### 메서드 축약 표현

function 을 축약한 표현이 가능하다

```javascript
const obj = {
  sayhi() {
    console.log("hi");
  },
};
```

#### reference

