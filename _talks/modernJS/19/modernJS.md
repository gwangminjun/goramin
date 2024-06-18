---
title: "[모던 자바 스크립트] 19장 프로토 타입"
collection: talks
type: "Talk"
permalink: _talks/modernJS/19/modernJS
date: 2024-04-07
---

## 19장 프로토 타입

자바스크립트는 명령형, 함숳평, 프로토타입기반, 객체지향 을 지원하는 멀티 패러다임 프로그래밍언어이다

### 클래스

ES6 에서 클래스가 도입되었다. 사실 클래스도 함수이며 기존 프로토타입 기반 패턴의 문법적 설탕이라고 설명가능하다

### 절차지향 프로그래밍

프로그램을 명령어 또는 함수의 목록으로 본다

### 객체지향 프로그래밍

여러개의 독립적인 단위, 즉 객체의 집합으로 프로그램을 표현한다<br>
실세게의 실체를 인식하는 철학적 사고를 프로그래밍에 접목한다<br>
실체는 특징이나 성질을 나타내는 속성을 가지고있다 이를 통해 실체를 인식하거나 구별한다 <br>
다양한 속성중에서 프로그램에 필요한 속성만을 간추려 표현하는것을 <b>추상화</b> 라고 한다

```javascript
const person = {
  name: "min",
  age: 25,
};
```

해당 객체는 이름과 주소를 속성으로 가지며 이를 가지고 다른객체와 구별하여 인식할수 있다 . 이처럼 속성을 통해 여러개의 값을 하나의 단위로 구성한 복합적인 자료구조를 객체라고 칭한다

### 상속과 프로토타입

```javascript
function Circle(radius) {
  this.radius = radius;
  this.getArea = function () {
    return Math.PI * this.radius ** 2;
  };
}

const test1 = new Circle(1);
const test2 = new Circle(2);

test1.getArea();
test2.getArea();

test1.getArea == test2.getArea; // false
```

만일 해당상황에서 getArea를 작동시 동일한 내용의 메서드를 사용하지만 생성자 함수는 인스턴스를 생성할때마다 동일 내용의 메서드를 중복 생성하고 모든 인스턴스가 중복 소유한다. <br>
이러한 상황은 불필요하게 메모리를 낭비한다 <br>
이러한 불필요한 중복을 제거하기위해 자바스크립트는 프로토타입을 기반으로 상속을 구현한다.

```javascript
function Circle(radius) {
  this.radius = radius;
}

Circle.prototype.getArea = function () {
  return Math.PI * this.radius ** 2;
};

const test1 = new Circle(1);
const test2 = new Circle(2);

test1.getArea();
test2.getArea();

test1.getArea == test2.getArea; // true
```

생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입, 상위(부모)객체역할을 하는 프로토타입의 모든 프로퍼티와 메서드를 상속받는다

### 프로토타입 객체

프로토타입 객체는 객체간 상속을 구현하기 위해 사용된다 <br>
프로토타입은 어떤객체의 상위객체 역할을 하는 객체로서 다른객체에 공유프로퍼티를 제공한다 <br>
모든 객체는 [[Prototype]] 이라는 내부슬롯을 가지며 이 내부슬롯의 값은 프로토타입의 참조다 <br>
프로토타입은 객체 생성방식에 의해 결정된다

### (\_proto\_\_) 접근자 프로퍼티

모든 객체는 \_proto\_\_ 접근자 프로퍼티를 통해 자신의 프로토타입 내부슬롯에 간접적으로 접근할수 있다

### (\_proto\_\_) 접근자 프로퍼티는 상속을 통해 사용한다

(\_proto**) 접근자 프로퍼티는 객체가 직접 소유하는 프로퍼티가 아니라 object.prototpye의 프로퍼티이다. <br>
모든 객체는 상속을 통해 object.prototpye.**proto\_\_ 접근자 프로포티를 사용할수 있다

```javascript
const person = { name: "lee" };

person.hasOwnProperty("__proto__"); // false
//모든객체는 __proto__ 프로퍼티를 소유하지 않는다

Object.getOwnPropertyDescriptor(Object.prototype, "__proto__"); //true

console.log({}.__proto__ === Object.prototype);
// 단 모든 객체는 접근자프로퍼티를 상속받아 사용할수 있다
```

모든 객체는 프로토타입의 계층구조인 프로토타입 체인에 묶여있다.
<br> 객체의 프로퍼티에 접근하려할때 해당 객체에 접근하려는 프로퍼티가 없다면 \__proto_ 접근차 프로퍼티가 가리키는 참조를 따라 자신의 부모역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다
<br> 결국 object.prototype 프로퍼티와 메서드는 모든 객체에 상속된다

### (\_proto\_\_) 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유

```javascript
const parent = {};
const child = {};

parent.__proto__ = child;
child.__proto__ = parent;
```

프로토타입은 단방향 링크드 리스트로 구현되어야 하지만 위 의 상황과 같이 서로가 자신의 프로토타입이 되는 순환 참조하는 프로토타입 체인이 생성되면 체인종점에 아무것도 존재하지않기 때문에 프로퍼티 검색시 무한루프에 빠진다
<br>이러한 상황을 방지하기위해 접근자프로퍼티를 통해 접근하고교체하게구현되어있다

### 프로토타입 접근자 프로퍼티를 코드내에서 사용하는것을 권장하지않는이유

모든객체가 프로토타입 접근자 프로퍼티를 사용할수는없다 (object)
고로 Object.getPrototypeOf 사용을 권장한다

### 함수객체의 prototype 프로퍼티

함수객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다
<br> 하지만 결국엔 객체의 proto 접근자 프로퍼티와 함수객만이 가지고있는 prototype 프로퍼티는 결국 동일한 프로토타입을 가리킨다
<br> 그렇지만 프로토타입을 사용하는 주체가 다르다

1. 객체 : 객체가 자신의 프로토타입에 접근 또는 교체하기위해 사용
2. 함수 : 생성자 함수가 자신이 생성할 객체의 프로토타입을 할당하기위해

```javascript
function test(name) {
  this.name = name;
}

const tt = new test("test");

test.prototype === tt.__proto__; // true
```

### 프로토타입의 construtor 프로퍼티와 생성자 함수

모든 프로토타입은 constructor 프로퍼티를 갖는다. 이 프로퍼티는 prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킨다

```javascript
function test(name) {
  this.name = name;
}

const tt = new test("test");

tt.construtor === test; // true
```

### 리터럴로 생성된 객체의 생성자 함수 및 프로토타입

리터럴 표기법으로 생성된 객체의 construtor 프로퍼티가 가리키는 생성자함수는 무엇일까

```javascript
const tt = {};

tt.construtor === object; // true
```

객체리터럴에 의해 생성된객체도 사실 object 생성자 함수와 연결되어있다 이 이유는 객체리터럴로 객체를 생성할때를 확인해야하는데
<br>object 생성자 함수를 생성시에 인수를 전달하지않거나 undefined 또는 null 을 인수로 전달하면서 호출시에 내부적으로 추상연산을 호출하여 object.prototype을 프로토타입으로 갖는 빈객체를 생성한다.

결국엔 리터럴 표기법에 의해 생성된 객체의 생성자함수와 생성자함수를 통해서 생성된객체의 생성자 함수는 같다

### 프로토타입의 생성시점

프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성된다

### 빌트인 생성자 함수

object,string,Number 등등 빌트인 생성자함수도 일반함수와 마찬가지로 비트인 생성자 함수가 생성되는 시점에 프로토타입이 생성된다

### 전역객체

코드가 실행되기 이전단계에 자바스크립트 엔진에 의해 생성되는 특수한 객체이다
<br> 클라이언트 사이드 환경에서는 window
<br> 서버사이트 환경에서는 global 객체를 의미한다

전역객체는 표준 빌트인 객체들과 환경에 따른 호스트 객체 그리고 var로 선언한 전역변수와 전역함수를 프로퍼티로 갖는다

### 객체리터럴 생성 객체과 object 생성자 함수 객체의 차이

객체 리터럴 방식은 객체 리터럴 내부에 프로퍼티를 추가하지만
<br> object 생성자 함수는 일단 빈객체를 생성한 이후 프로퍼티를 추가한다

### 프로토타입 체인

일단 언제나 프로토타입의 프로토타입은 object.prototype이다
객체의 프로퍼티에 접근하려할때 해당 객체에 접근하려는 프로퍼티가 없다면 자신의 부모역할을 하는 프로토타입의 프로퍼티를 순차적으로 검색한다 이를 <b>프로토타입 체인</b> 이라고 한다 프로토타입 체인을 통해서 자바스크립트는 객체지향 프로그래밍의 상속을 구현한다.

프로퍼티가 아닌 식별자를 검색하는 경우에는 스코프 체인을 사용하며 식별자가 선언된 스코프를 기준으로 식별자를 검색한다음 검색한 식별자의 객체의 프로토타입 체인을 통하여 프로퍼티를 검색한다.

### 오버라이딩 과 프로퍼티 섀도잉

```javascript
const person = (function (radius) {
  this.radius = radius;

  person.prototype.getArea = function () {
    return Math.PI * this.radius ** 2;
  };

  return Circle;
})();

const me = new person("Lee");

me.getArea = function () {
  console.log("override");
};

me.getArea(); // 'override'
```

해당 예시는 생성자 함수로 인스턴스(객체)를 생성한 다음 인스턴스에 메서드를 추가했다
<br> 이처럼 프로토타입 프로퍼티와 같은 이름의 프로퍼티를 인스턴스에 추가하면 프로토타입 프로퍼티를 검색하여 프로토타입 프로퍼티를 덮어쓰지않고 인스턴스 프로퍼티로 추가한다.
이를 오버라이딩(재정의)이라고 한다. 이로 인해 프로토타입 프로퍼티가 가려지는것을 프로퍼티 섀도잉 이라고 한다

해당 인스턴스의 프로퍼티를 삭제하는 경우 당연히 인스턴스의 프로퍼티가 삭제되고 하위객체를 통해 프로토타입의 프로퍼티를 변경또는 삭제하는것은 불가능하다

### 프로토타입의 교체

1. 생성자 함수

```javascript
const person = (function () {
  function person(name) {
    this.name = name;
  }
  person.prototype = {
    constructor: person,
    sayhello() {
      console.log("hi");
    },
  };

  return person;
})();
```

이러처럼 프로토타입을 생성자함수로 교체하는경우 constructor 프로퍼티와 생성자 함수의 연결이 파괴되므로 constructor프로퍼티를 추가해야한다

```javascript
const person = (function () {
  function person(name) {
    this.name = name;
  }
  person.prototype = {
    constructor: person,
    sayhello() {
      console.log("hi");
    },
  };

  return person;
})();
```

2. 인스턴스
   인스턴스의 프로토타입 접근자 프로퍼티를 통해 프로토타입을 교체 가능하다<br>
   이렇게 변경할경우 미래에 생성할 인스턴스의 프로토타입을 교체하는 경우다. 이역시 이런식으로 변경할경우 생성자함수를 검색시에는 object가 나온다 하지만 이경우에는 construtor을 선언할수 없기에 object로 프로토타입이 된다.

### instanceof

우변의 생성자 함수의 prototype에 바인딩 된 객체가 좌변의 객체의 프로토타입 체인 상에 존재하면 true 아닌경우 false

```javascript
function person(name) {
  this.name = name;
}

const me = new person("ymj");

me instanceof person; // true
```

### 직접상속

1. object.create
   object.create(a, b, c)
   <br> a: 생성할 객체의 프로토타입으로 지정할 객체
   <br> b: 생성할 객체의 포로퍼티를 갖는 객체
   <br> c: 지정된 프로토타입 및 프로퍼티를 갖는 새로운 객체
   이 처럼 객체를 생성하면서 매개변수로 상속옵션을 받아 상속을 구현한다 이 메서드를 통해서는 프로토타입 체인의 종점에 위치하는 객체를 생성할수 있다.

2. 객체 리터럴 내부에서 프로토타입 접근자 프로퍼티를 사용한 상속

```javascript
const proto = { a: "1" };

const obj = {
  b: "2",
  __proto__: proto,
};
```

### 정적 프로퍼티/메서드

정적 프로퍼티/메서드는 생성자 함수로 인스턴스를 생성하지 않아도 참조/호출 할수 있는 프로퍼티/메서드이다

```javascript
function person(name) {
  this.name = name;
}

//정적 프로퍼티
person.staticProp = "static Prop";

//정적 메서드
person.staticMethod = function () {
  console.log("static Method");
};

person.staticProp();

person.staticMethod();
```

person 생성자 함수는 객체 이므로 자신의 프로퍼티/메서드를 소유할수있는데 이를 정적 프로퍼티/메서드라고 한다.
<br> 이 프로퍼티와 메서드는 인스턴스로 호출할수 없다

### 프로퍼티 존재 확인

```javascript
key in object; // 1

Object.prototype.hasOwnProperty; // 2
```

### 프로퍼티 열거

1. for in 문

```javascript
for (key in object) {
}
```

하지만 for in 을 순회해도 열거 될수 없는 메서드가 존재하는데 열거할수 없이 enumerable 값이 false로 정의 되있는 메서드는 열거 할수없다.

고로 fon in 문은 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로퍼티 중에서 프로퍼티 어트리뷰트 enumerable 값이 true 인 프로퍼티를 순회하면 열거한다

2. object.keys/values/entries 메서드
   객체 자신의 고유 프로퍼티만을 열거하기위해서는 해당 메서드를 사용한다.

### call 메서드

this로 사용할 객체를 전달하면서 함수를 호출한다.

#### reference

