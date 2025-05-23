---
title: "[모던 자바 스크립트] 8장 타입변환"
collection: talks
type: "Talk"
permalink: _talks/modernJS/8/modernJS
date: 2024-03-02
---

# 8장 타입변환

---

## 개요
변수의 타입을 변환
1. 명시적 타입변환 , 타입 캐스팅
  - 개발자가 의도적으로 값의 타입을 변환
2. 암묵적 타입변환 , 타입 강제 변환
  - 개발자의 의도와 상관없이 암묵적으로 타입이 자동변환

### 타입 변환 과정
- 타입변환 시 기존의 원시값을 직접 변경하는것은 아니다.
- 원시값은 변경 불가능한 값으로  변경할수 없다.
- 타입변환이란 기존의 원시값을 사용해 다른 타입의 새로운 원시값을 생성하는 것 이다.

```javascript
var x = 10
var str = x + '';
console.log(typeof str, str); // string 10

console.log(typeof x, x);     // number 10
```
위 예시의 경우
1. 표현식 x + '' 의 평가를 위해 x 변수값의 숫자값을 바탕으로 새로운 문자열값 '10' 생성
2. 생성된 값으로 표현식을 평가 ,  이때 문자열 10은 x에 재할당되지않음
3. 피연산자의 값을 암묵적으로 타입 변환해 새로운 타입의 값을 만들어 한번 사용후 버린다.


### 암묵적 타입 변환
1. 문자열 타입
2. 숫자 타입
3. 불리언 타입
- 불리언 타입이 아닌 값을 truthy 또는 falsy 값으로 구분
- falsy 값
  - false,undefined,null,NaN,''

### 명시적 타입 변환
1. 문자열 타입
  - String 생성자 함수를 new 연산자 없이 호출하는 방법
  - Object.prototype.toString 메서드를 사용하는 방법
  - 문자열 연결 연산자를 이용하는 방법
2. 숫자 타입
  - Number(’0’);
  - parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
  - + 단항 산술 연산자를 이용하는 방법
  - * 산술 연산자를 이용하는 방법
3. 불리언 타입
  - Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
  - ! 부정 논리 연산자를 두 번 사용하는 방법

# 단축평가
## 개요
표현식을 평가하는 도중에 평가결과가 확정된 경우 나머지 평가 과정을 생략

```javascript
    true || A // true
    false || A // A
   true && A // A
   false && A // False
```

### 옵셔널 체이닝 (?.)
- 좌항의 피 연산자가 null 또는 undefined 인 경우 undefined 반환 아니면 우항 참조
- 변수의 null 체크시 사용

### null 병합 연산자 (??)
- 좌항의 피 연산자가 null 또는 undefined 인 경우 우항 , 아니면 좌항
- 변수의 기본값 설정시 사용

#### reference

