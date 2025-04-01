---
title: "[모던 자바 스크립트] 17장 생성자 함수에 의한 객체 생성"
collection: talks
type: "Talk"
permalink: _talks/modernJS/17/modernJS
date: 2024-03-29
---

# 17장 생성자 함수에 의한 객체 생성

---

### 생성자함수

```javascript
const test = new Object();
```

빈객체를 생성하여 반환한다.<br>
생성자 함수에 의해 생성된 객체를 인스턴스라고 칭한다

### 생성자 함수의 장점

객체 리터럴에 의한 객체 생성방식은 직관적이고 간편하지만 <br>
하나의 객체만을 생성하기 때문에 객체를 여러개 생성할경우 매번 같은 프로퍼티를 기술해야한다<br>

생성자 함수를 사용하면 여러개의 객체를 간편하게 생성할수 있다

```javascript
function person(test) {
  this.test = test;
}

const person1 = person(1);
const person2 = person(2);
```

### 생성자 함수의 인스턴스 생성 과정

1. 인스턴스 생성과 this 바인딩

- 암묵적으로 빈 객체가 생성되고 빈객체(인스턴스)는 this에 바인딩된다

2. 인스턴스 초기화

- 생성자 함수에 기술되어있는 코드가 실행되며 this에 바인딩 되어 있는 인스턴스를 초기화한다
- 프로퍼니타 메서드를 추가하고 프로퍼티는 할당하여 초기화한다

3. 인스턴스 반환

- 생성자 함수 내부의 모든처리가 끝나면 완성된 인스턴스가 바인딩된 this에 반환된다
- return 값이 존재 할경우 this대신 해당 return 값이 반환된다

### 함수 호출

함수는 객체이지만 일반객체와 다르다. 일반객체와 다르게 함수는 호출할수 있다 <br>
함수로서 동작하기위해 함수객체만을 위한 내부메서드와 내부 슬롯을 추가로 가지고있다

```javascript
function person() {}

//일반적인 함수로서 호출 : [[call]]
person();

// 생성자 함수로서 호출 : [[Construct]]
new person();
```

[[call]]를 가진 함수를 callable 이라하며 <br>
[[Construct]]를 가진 함수를 Constructor 이라한다<br>
[[Construct]]를 갖지않은 함수객체는 생성자함수로서 호출할수 없다

결론 : 모든 함수객체는 반드시 callable이지만 모든 함수객체가 Constructor은 아니다

### new 연산자

new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다

### new.target

함수내부에서 new.target을 사용하면 new 연산자와 함께 생성자 함수로서 호출되었는지 확인할수 있다<br>
new 연산자화 함께 생성자 함수로서 호출되면 new.target은 함수 자신을 가리킨다



#### reference

