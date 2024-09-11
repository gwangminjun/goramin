---
title: "[우아한 타입스크립트 with 리액트] 2장 타입"
collection: talks
type: "Talk"
permalink: _talks/woowahanTS/2/content
date: 2024-08-18
---

## 2장 타입

## 이슈
### 2.2.5_"식별할 수 있는 유니온"이란 무엇인지 설명해주세요. (p49)

=============================================================
## 리터럴 타입
정해진 값을 갖는것

## 유니온 타입 (OR 연산자(||))
값이 정해져 있지 않고 <br>
A이거나 B이다  OR 연산자(||)

### 정의방식
- 연산자 (|)를 이용 
→ 타입을 여러 개 연결하는 방식

```JS
function logText(text: string | number) {
  // ...
}
```

### 식별가능한 유니온 타입
동일한 속성의 타입을 다르게 해서 구분가능

검사 항목수에 따른 추천되는 조건문
- 적은 경우 : if 문
- 많은 경우 : switch 문


예시
```ts

interface Cat {
  name: "Cat";
  sound : "야옹"
  meow(): void;
}

interface Dog {
  name: "Dog";
  sound : "멍멍"
  bark(): void;
}

//this.sound를 통해 인터페이스의 sound를 가져오고 싶었지만 
//실제 구현은 클래스나 객체에서 이루어져야 하기 때문에 클래스 선언 후 사용하였습니다

class CatImp implements Cat {
  name = "Cat";
  sound = "야옹";

  meow() {
    console.log(this.sound);
  }
}

class DogImp implements Dog {
  name = "Dog";
  sound = "멍멍";

  bark() {
    console.log(this.sound);
  }
}

function Klaxon(resource: Cat | Dog) {
  console.log(resource.sound); 

  if (resource.name === 'Cat'){
    const cat = new CatImp();
    cat.meow();
  } else {
    const dog  = new DogImp();
    dog.bark();
    }
    
}
```

## 인터섹션 타입(Intersection Type) (AND)
여러 개의 타입을 하나로 합쳐주는 역할.<br>
필요한 모든 기능을 가진 하나의 타입

### 정의방식
- 연산자(&) 이용
- 모든 속성 기입 필수

```ts
interface Person {
  name: string;
  age: number;
}
interface Developer {
  name: string;
  skill: number;
}
type Capt = Person & Developer;
{
  name: string;
  age: number;
  skill: string;
}
```

### refernce
- https://velog.io/@katej927/TypeScript-%EC%97%B0%EC%82%B0%EC%9E%90%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%ED%83%80%EC%9E%85-%EC%A0%95%EC%9D%98#-%EB%A6%AC%ED%84%B0%EB%9F%B4-%ED%83%80%EC%9E%85-literal-type

=============================================================

### enum 타입의 특징과 사용방법은 무엇이고 enum 타입을 트리쉐이킹 할 수 있는 방법은 무엇인가요? (57p)

=============================================================
## Enum
- 특정 값(상수)들의 집합
- 특정 값을 고정하는 또다른 독립된 자료형

### 인덱싱
- 기본적으로 enum은 0부터 시작하여 멤버들의 번호를 매긴다
```ts
enum Week {
  Sun, // 0
  Mon, // 1
  Tue, // 2
  Wed, // 3
  Thu, // 4
  Fri, // 5
  Sat  // 6
}
```

### 상수
enum을 사용하면 컴파일 후에도 객체가 남는다

해당 특징 때문에 번들 파일이 불필요하게 커질수 있다는 단점이 있다.

```ts
enum Bool {
  True,
  False,
  FileNotFound
}
let value = Bool.FileNotFound;

//컴파일

var Bool;
(function (Bool) {
  Bool[(Bool["True"] = 0)] = "True";
  Bool[(Bool["False"] = 1)] = "False";
  Bool[(Bool["FileNotFound"] = 2)] = "FileNotFound";
})(Bool || (Bool = {}));
let value = Bool.FileNotFound;
```

const Enum을 사용
```ts
const enum Bool {
  True,
  False,
  FileNotFound
}
let value = Bool.FileNotFound;

//컴파일

let value = 2; /* FileNotFound */
```

### reverse mapping
객체에서 키와 값의 위치를 바꿔서 새로운 객체를 생성

숫자형 enum 에서만 사용가능
```ts
enum Enum {
  A
}
let a = Enum.A; // 키로 값을 획득 하기
let keyName = Enum[a]; // 값으로 키를 획득 하기
```

## 트리쉐이킹
트리 쉐이킹은 사용하지 않는 코드를 제거하는 방식

Tree-shaking을 통해서 빌드 시스템을 구성하면 export 했지만 아무데서도 import 하지 않은 모듈이나 사용하지 않는 코드를 삭제해서 번들 크기를 줄여서 렌더링 시간을 줄일 수 있다.

### enum 트리쉐이킹
#### enum이 트리쉐이킹 되지 않는 이유
Typescirpt  컴파일러는 이를 IIFE(즉시실행 함수)로 구현을 해냈다.  <br>
Rollup과 같은 번들러는 IIFE를 사용하지 않는 코드라고 판단할 수 없어서 <br>
Tree-shaking이 되지 않는다.


#### enum의 트리쉐이킹 시도

const enum 사용
```ts
const enum MOBILE_OS {
    IOS = 'iOS',
    ANDROID = 'Android',
}
const ios = MOBILE_OS.IOS

// 트랜스 파일

const ios = "iOS" /* IOS */;
```

Tree-shaking이라는 관점에서는 Union Types와 같습니다. <br>
사용하지 않는다면 번들에 포함되지 않습니다. <br>
하지만 긴 문자열을 할당하는 경우에는 Union types와 비교해 다소 불리한 점이 있다 <br>

```ts
// TypeScript
const enum NAME {
  JUGEM = '寿限無寿限無五劫の擦り切れ海砂利水魚の…', // 일본에서 '김수한무 거북이와 두루미 삼천갑자 동방삭...'과 비슷한 용도로 사용하는 긴 이름입니다.
TARO = '다로', 
JIRO = '지로', 
} 
const isJugem = name === NAME.JUGEM
 
// JavaScript 트랜스파일 후
const isJugem = name === "u5BFFu9650u7121u5BFFu9650u7121u4E94u52ABu306Eu64E6u308Au5207u308Cu6D77u7802u5229u6C34u9B5Au306Eu2026" /* JUGEM */;
```


const enum은 TypeScript가 트랜스파일(transpile)할 때 컴파일 타임에 값으로 치환하는 방식으로 작동 <br>
즉, 런타임에 const enum이 실제로 존재하는 것이 아니라, 그 값을 코드 내에서 직접 사용하는 방식으로 변환

NAME.JUGEM을 사용하면, 컴파일된 자바스크립트에서는 NAME.JUGEM 대신 이 긴 문자열이 그대로 들어가게 됩니다

const enum의 트리쉐이킹 최적화 저해
1. 상수 치환: 트랜스파일 후 이 긴 문자열은 코드 여러 곳에 직접 치환됩니다. 이 과정에서 문자열 상수가 여러 곳에 복사되어 들어가게 됩니다.
2. 사용된 문자열 유지: 트리 쉐이킹은 사용되지 않는 코드를 제거하는 것이 목표인데,
   이 긴 문자열이 여러 곳에서 사용된다고 판단되면 트리 쉐이킹이 해당 문자열을 제거하지 못합니다.
3. 번들 크기 증가: 긴 문자열이 여러 군데에서 사용될수록, 최종 번들 파일 크기가 증가합니다. 특히 이 경우, 매우 긴 문자열이 코드에 여러 번 복사되면 파일 크기에 부정적인 영향을 미치게 됩니다.




### reference
- https://inpa.tistory.com/entry/TS-%F0%9F%93%98-%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-enum-%EC%A0%95%EB%A6%AC
- https://joshua1988.github.io/ts/guide/enums.html#%EB%A6%AC%EB%B2%84%EC%8A%A4-%EB%A7%A4%ED%95%91-reverse-mapping
- https://velog.io/@hhhminme/%EB%84%A4-Enum-%EB%88%84%EA%B0%80-Typescript%EC%97%90%EC%84%9C-Enum%EC%9D%84-%EC%93%B0%EB%83%90
- https://engineering.linecorp.com/ko/blog/typescript-enum-tree-shaking

=============================================================
## 이터러블의 개념과 장점은 무엇인가요? (61p)

## 정의

iterate : (계산, 컴퓨터 처리 절차를) 반복하다
iterator : 반복자

### iterable
iterator를 리턴하는 [Symbol.iterator]() 메서드를 가진 객체
자료를 반복할 수 있는 객체

### iterator
{value : 값 , done : true/false} 형태의 iterator 객체를 리턴하는 next() 메서드를 가진 객체.
next 메서드로 순환 할 수 있는 객체


## 장점
1. 메모리 효율성
   지연 평가(Lazy Evaluation)
   이터러블은 데이터를 미리 모두 메모리에 로드하지 않고, 필요할 때마다 한 요소씩 계산하거나 가져오는 방식으로 동작
    ```ts
    function* infiniteNumbers() {
      let num = 0;
      while (true) {
        yield num++;
      }
    }
    ```
    이터러블은 한 번에 하나씩 데이터를 처리하므로,<br>
    매우 큰 데이터를 다룰 때 메모리 사용을 최소화 가능 <br>
    매우 큰 데이터가 있는 배열을 한 번에 처리하는 대신, <br>
    이터러블을 사용하여 한 번에 하나씩 처리하면 메모리를 크게 절약할 수 있습니다.<br>


2. 이터레이션 문법 사용
   이터러블 프로토콜을 따르는 객체라면 for...of 문과 같은 이터레이션 문법을 사용하여 <br>
   자료 구조간 상호 운용성을 높일수 있습니다.
    ```ts
    const array = [1, 2, 3];
    for (const value of array) {
      console.log(value);
    }
    ```

## 추가
java는 각 자료구조를 표준화한 아키텍처인 Java Collection Framework 의 최상위 인터페이스로 이터러블을 구현하고 있습니다
![image](https://github.com/user-attachments/assets/7766437f-010f-49ad-8dbd-8e23800651fb)


### reference
- https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9D%B4%ED%84%B0%EB%9F%AC%EB%B8%94-%EC%9D%B4%ED%84%B0%EB%A0%88%EC%9D%B4%ED%84%B0-%F0%9F%92%AF%EC%99%84%EB%B2%BD-%EC%9D%B4%ED%95%B4

=============================================================

## 2.2.8_어떤 상황에서 어떤 키워드의 타입을 사용해야 좋을까요? (60p)

## 개념
1. type
    - 타입의 새로운 이름을 만드는것
    - 상속이 불가능 하기때문에 유연한 코드 작성을 위해서 인터페이스 사용을 권장
2. interface
    - 객체의 구조를 정의하기 위해 사용되는 예약어
    - 인터페이스에 선언된 프로퍼티 또는 메서들의 구현을 가제해 일관성을 유지
    - 객체의 구조를 정의하지만, 메서드 구현을 직접 포함하지는 않습니다.
3. class
    - 속성과 메서드에 대한 타입을 명시할 수 있다.
    - 객체 지향 개념을 구현하기 위해 사용
    - 상속 가능
4. enum
    - 열거형
    - 특정 값들의 집합
    - 상수값을 대신하여 사용함


## 사용
```ts
//1. type
type Person = {
  id: number;
  name: string;
  email: string;
}

//2. interface
//상속
interface Person {
    name: string;
    age: number;
}

interface Developer extends Person {
    language: string;
}

const person: Developer = {
    language: "TypeScript",
    age: 28,
    name: "minjun",
}

//3. class 
//상속
class Animal {
    move(distanceInMeters: number): void {
        console.log(`${distanceInMeters}m 이동했습니다.`);
    }
}

class Dog extends Animal {
    speak(): void {
        console.log("멍멍");
    }
}

class Cat extends Animal {
    speak(): void {
        console.log("야옹");
    }
}

const dog = new Dog();
dog.move(10); // 10m 이동했습니다.
dog.speak(); // 멍멍

const cat = new Cat();
Cat.move(15); // 15m 이동했습니다.
Cat.speak(); // 야옹

//4. enum
enum Computer {
  Monitor = 3,
  Mouse = 7,
  Keyboard = 1,
  Speaker = 5,
}

let a: Computer = Computer.Keyboard;
let b: number = Computer.Mouse;

console.log(a); // 1
console.log(b); // 7
```

### reference
- https://velog.io/@coding0206/TypeScript-Enum-Interface-TypeClass
- https://summerr.tistory.com/83

=============================================================

## 2.2.4 JS의 덕 타이핑, 타입스크립트의 구조적 타이핑의 공통점 및 차이점은 어떤 것들이 있을까요? (46p ~ 48p)

## 덕타이핑

만약 오리처럼 걷고 오리처럼 꽥 소리를 낸다면, 그것은 분명히 오리이다.

변수에 어떠한 타입의 값도 할당할 수 있는것

ts : 여러 타입을 조합한 새로운 타입을 가지는것

### 타입스크립트에서 덕 타이핑 사용
#### 유니온 타입
```ts
type Team = "Red" | "Blue"
```
#### 제네릭 타입
어떠한 타입이든 정의될 수 있지만 호출되는 시점에 타입이 결정
```ts
function ide<T> (arg:T):T{
    return arg;
}
```


## 구조적 타이핑

타입이 특정 구조를 가지면 그 타입으로 취급

### 타입스크립트에서 구조적 타이핑 사용
#### DB에 따른 유닛 테스트 작성
```ts
// 추상적인 interface를 만들고, 
// 상속이 아닌 구조적 타이핑으로 PostgresDB, FirebaseDB 등 
// 다양한 DB에 대한 구조 검증
interface Author {
  first: string;
  last: string;
}

interface DB {
  runQuery: (sql: string) => any[]; //결과를 이차원 배열로 반환
}

function getauthors(database: DB): Author[] {
  const authorRows = database.runQuery(`SELECT FIRST, LAST FROM AUTHORS`); //이차원 배열 획득
  return authorRows.map(row => ({ first: row[0], last: row[1] }); // Author 구조에 맞게 변환하여 반환
}

//유닛 테스트
test('getAuthors', () => {
  const authors = getAuthors({
    runQuery(sql: string) {
      return [['Toni', 'Morrison'], ['Maya', 'Angelou']];
      // 가짜 DB 객체 사용
    }
  });
  //바른 형태의 Author 배열을 반환하는지를 검증
  expect(authors).toEqual([
    {first: 'Toni', last: 'Morrison'},
    {first: 'Maya', last: 'Angelou'}
  ]);
});
```

### 덕 타이핑 과 구조적 타이핑 공통점
1. 구조기반 타입 판단
    - 객체의 실제 구조 기반 판단
2. 유연성
    - 명시적인 상속관계 없이도 동일한 프로퍼티와 메서드를 가진 객체는 그 타입으로 인정


### 덕 타이핑 과 구조적 타이핑 차이점
1. 타입 검증 시점
    - 덕 타이핑 : 런타입 시점에 타입을 확인
    - 구조적 타이핑 : 컴파일 시점에 타입 확인
2. 정적 분석
    - 덕 타이핑 : 런타임 시점에 타입을 확인 -> 런타입 오류 증가
    - 구조적 타이핑 : 코드 작성 시점에 타입 검증을 수행하기 때문에 런타임 오류가 적다
### reference
- https://kfdd6630.tistory.com/entry/js-%EB%8D%95-%ED%83%80%EC%9D%B4%ED%95%91duck-typing#google_vignette
- https://openmaker.tistory.com/142
- https://en.wikipedia.org/wiki/Duck_typing
- https://en.wikipedia.org/wiki/Structural_type_system

=============================================================

## 2.4.4. type과 interface 키워드의 차이점은 무엇인가요? ( 74p ~ 76p)
## 상속
### interface
extends 키워드를 이용
```ts
interface Person {
  name: string;
  age: number;
}

interface developer extends Person { // 확장(상속)
  language: string;
}

const minjun: developer = {
  name: 'minjun',
  age: 28,
  language: 'java'
}
```
### type
교차 타입(&)을 이용
```ts
type Person = {
  name: string,
  age: number
}

type developer = Person & { // 확장(상속)
  language: string
}

const jieun: Student = {
  name: 'jieun',
  age: 27,
  school: 'HY'
}
```

## computed value
- computed value : 표현식을 이용해서 객체의 key 값을 정의
### interface
computed value 사용 불가
```ts
type Subjects = 'math' | 'science' | 'sociology';

interface Grades {
  [key in Subjects]: string; // ❗️Error: A mapped type may not declare properties or methods.
}
```
### type
computed value 사용 가능
```ts
type Subjects = 'Math' | 'Science' | 'Sociology';

type Grades = {
  [key in Subjects]: string;
}
```

### 사용
정해진 컨벤션이 있다면 해당 컨벤션을 사용하고 <br>
없다면 각 특징을 파악하여 사용해야할 시점에 특징에 맞게 사용하면 될거같습니다~

### reference
- https://velog.io/@wlwl99/TypeScript-type%EA%B3%BC-interface%EC%9D%98-%EC%B0%A8%EC%9D%B4
- https://velog.io/@1998yuki0331/%EB%82%98-%EB%B3%B4%EB%A0%A4%EA%B3%A0-%EC%A0%95%EB%A6%AC%ED%95%98%EB%8A%94-TypeScript-%ED%95%B8%EB%93%9C%EB%B6%81

=============================================================

