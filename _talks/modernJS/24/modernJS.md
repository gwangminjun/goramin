---
title: "[모던 자바 스크립트] 24장 클로저"
collection: talks
type: "Talk"
permalink: _talks/modernJS/25/modernJS
date: 2024-05-05
---

### 24장 클로저

클로저는 자바스크립트 고유의 개념이 아니다
<br> 함수를 일급 객체로 취급하는 함수형 프로그램 언어 에서 사용되는 중요한 특성이다.

### 렉시컬스코프

자바스크립트는 함수를 어디서 호출했는지가 아니라 함수를 어디에 정의했는지에 따라 상위스코프를 결정한다 <br> 이를 렉시컬 스코프(정적 스코프)라 칭한다

결론은 렉시컬 환경의 외부 렉시컬 환경에 대한 참조에 저장할 참조값 즉 상위 스코프에 대한 참조는 함수정의가 평가되는 시점에 함수가 정의된 환경(위치)
에 의해 결정된다

### 함수객체의 내부슬롯 [[Environment]]

자신의 정의된 환경에 상위 스코프를 기억하기위해 함수는 자신의 내부슬롯에 자신이 정의된 환경을 즉 상위 스코프의 참조를 저장한다.
<br> 이때 저장된 상위 스코프의 참조는 현재 실행중인 실행 컨텍스트의 렉시컬 환경을 가리킨다
<br> 왜냐면 함수 정의가 평가되어 함수 객체를 생성하는시점은 함수가 정의된 환경, 즉 상위 함수가 평가 또는 실행되고 있는 시점이며 이때 현재 현재 실행중인 실행 컨텍스트는 상위 함수의 실행 컨텍스트 이기 때문이다

### 클로저와 렉시컬 환경

```javascript
const x = 1;

function outer() {
  const x = 10;
  const inner = function () {
    console.log(x);
  };
  return inner;
}

const innerFunc = outer();
innerFunc(); // 10
```

위의 예시에서 outer 함수는 inner 함수를 리턴하고 제거(pop)된다 <br>
하지만 코드의 실행결과는 outer 함수내에서 선언한 10을 가리키고 있는데
<br>이처럼 외부함수보다 중첩함수가 더 오래 유지되는 경우 중첩함수는 이미 생명주기가 종료된 외부함수의 변수를 참조할수 있다
<br>이를 클로저라고 칭한다

outer 함수의 실행이 종료되면 outer 함수의 실행 컨텍스트는 실행 컨텍스트 스택에서 제거된다
<br> 하지만 outer 함수의 렉시컬 환경까지 소멸하는것은 아니다
<br> outer 함수의 렉시컬환경은 inner 함수의 [[Environment]] 내부슬롯에 의해 참조되어 있기 때문에 가비지 컬렉션의 대상이 되지 않기 때문이다

### 클로저 함수

이론적으로 이처럼 자바스크립트이 모든함수는 상위 스코프를 기억하므로 모든 함수는 클로저이다 하지만 일반적으로 모든 함수를 클로저라고는 하지않는다.

만약 중접함수가 상위 스코프의 어떤 식별자도 참조하지않는다면 상위스코프를 기억하지않는다.

그러므로 클로저는 중첩함수가 상위 스코프의 식별자를 참조하고 있고 중첩함수가 외부함수보다 더 오래 유지되는 경우에 한정하는것이 일반적이다.

### 자유함수

클로저에 의해 참조되는 상위 스코프의 변수를 자유번수라고 부른다
<br> 클로저란 함수가 자유변수에 대해 닫혀 있다는 의미로 자유변수에 묶여있는 함수라고 할수 있다.

### 클로저의 활용

클로저는 상태를 안전하게 변경하고, 유지하기 위해 사용한다. 상태를 안전하게 은닉하고 특정함수에게만 상태변경을 허용하기위해 사용한다.

예제 1

```javascript
let num = 0;

const increase = function () {
  return ++num;
};

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

위 예제의 문제점은 동작은 문제가 없지만
카운트의 상태가 전역변수를 통해 관리되고 있기 때문에 누구나 접근할수 있고 변경할수 도있으며 그로인해 의도치않게 상태가 변경될수 있다.
이러한 전역변수를 increase 함수의 지역변수로 바꾸어보자

예제 2

```javascript
const increase = function () {
  let num = 0;
  return ++num;
};

console.log(increase()); // 1
console.log(increase()); // 1
console.log(increase()); // 1
```

위 예제의 문제점은 전역변수 num을 지역변수로 변경하여 상태변경은 방지했지만 increase 함수가 호출될때마다 지역변수 num은 다시 선언되며 0으로 초기화 되기 때문에 이전상태를 유지하지 못한다.

이러한 문제점은 클로저를 통하여 해결할수있다

```javascript
const  increase = (function() {
    let num = 0;

    return function (){
        return ++num;
    }
}();)

console.log(increase()); // 1
console.log(increase()); // 2
console.log(increase()); // 3
```

위코드를 싱행하면 즉시 실행 함수가 호출되고 즉시 실행함수가 increase 변수에 할당된다.

increase 변수에 할당된 함수는 자신이 정의된 위치에 결정된 상위 스코프인 즉시 실행함수의 렉시컬 환경을 기억하는 클로저이다.

즉시 실행함수는 호출된이후 소멸하지만 즉시 실행함수가 반환한 클로저는 increase 변수에 할당되어 자신이 정의된 위치에 따라 상위 스코프인 즉시 실행함수의 렉시컬환경을 기억하고 있다

따라서 클로저는 카운트 상태를 유지하기 위한 자유변수 num을 언제 어디서 호출하든지 참조하고 변경할수 있다

또한 즉시 실행함수는 한번만 실행되기때문에 num 변수가 재차 초기화 될 일은없으면

또한 num변수는 외부에서 직접 접근할수도 없기때문에 변경될 걱정도 할 필요가없다.

이처럼 클로저는 상태가 의도치 않게 변경되지않도록 안전하게 은닉하고 특정함수에게만 상태변경을 허용하여 상태를 안전하게 변경하고 유지하기 위해 사용한다.

변수값은 누군가에 의해 언제든지 변경될수 있어 오류발생의 근본적인 원인이 될수 있다.
외부 상태 변경이나 가변 데이터를 피하고 불변성을 지향하는 함수형 프로그래밍에서 부수효과를 최대한 억제하여 오류를 피하고 프로그램의 안정성을 높이기 위해서 클로저는 적극적으로 사용된다.

### 캡슐화와 정보은닉

캡슐화는 객체의 상태를 나타내는 프로퍼티와 프로퍼티를 참조하고 조작할수 있는 동작인 메서드를 하나로 묶는것을 의미한다.

캡슐화는 객체의 특정 프로퍼티나 메서드를 감출 목적으로 사용하기도 하는데 이를 정보 은닉이라고 한다.

정보은닉은 외부에 공개할 필요가 없는 구현의 일부를 외부에 공개되지않도록 감추어 적절치 못한 접근으로 부터 객체의 상태가 변경되는 것을 방지해 정보를 보호하고 결합도(객체간의 상호의존성)을 낮추는 효과가 있다

대부분의 객체지향 프로그래밍 언어는 클래스를 정의하고 그 클래스를 구성하는 멤버에 대하여 public, private, pretected 같은 접근 제한자를 선언하여 공개범위를 한정할수 있다.

자바스크립트는 기본적으로 접근 제한자를 제공하지 않아서 기본적으로 모든 프로퍼티와 메서드는 외부에 공개되어 있다.

하지만 클로저를 사용하여 즉시실행함수 패턴을 사용하면 정보은닉이 가능한것처럼 보인다.

하지만 즉시실행함수를 여러 인스턴스에 생성할경우 이전의 인스턴스의 값이 다른 인스턴스 값에 참조되기 때문에 완전하게 정보은닉을 지원하지는 않는다.



#### reference
