---
title: "[모던 자바 스크립트] 11장 원시 값과 객체의 비교"
collection: talks
type: "Talk"
permalink: _talks/modernJS/11/modernJS
date: 2024-03-10
---

# 11. 원시값과 객체의 비교

---

1. 원시값

- 변경 불가능한 값
- 원시값을 변수에 할당시 변수에는 실제값이 저장된다
- 원시값을 갖는 변수를 다른 변수에 할당시 원시값이 복사되어 전달
- (값에 의한 전달)

2. 객체 값

- 변경가능한 값
- 객체값을 변수에 할당시 변수에는 참조값이 저장된다
- 객체를 가리키는 변수를 다른변수에 할당시 참조값이 복사되어 전달
- (참조에 의한 전달)

### 원시값

변경 불가능한 값 == 읽기 전용 값 <br>
변경 불가능하다는 것은 변수가 아니라 값에 대한 진술이며, <br>원시 값 자체가 아닌 변수는 언제든지 재할당을 통해 값을 변경할수 있다

### 원시값 재할당

원시값을 을 할당한 변수에 새로운 원시값을 재할당 시엔 이전의 원시값 을 변경하는게 아니라 새로운 메모리 공간을 확보하고 재할당된 원시값을 저장한후 변수는 새롭게 재할당된 원시값을 가리킨다 <br>
이때 변수가 참조하던 메모리공간의 주소가 변경된다 <br>

만약 원시값이 변경 가능한 값인 경우 원시값 자체를 변경한다 <br>

이러한 특성으로 인해 예기치 않은 변수값의 변경이 가능함으로써<br> 값의 변경 즉 상태 변경을 추적하기 어렵게 만든다

### 문자열

원시값을 저장하려면 먼저 확보해야하는 메모리공간의 크기를 결정해야한다. <br>
이를 위해 원시 타입별로 메모리 공간의 크기가 미리 정해져 있다 <br>
문자열은 다른 원시 값과 비교 할때 독특한 특징이 있는데 <br>
문자열은 0개 이상의 문자(char)로 이루어져 있으며 1개의 문자는 2 바이트 메모리 공간에 저장된다 <br>

따라서 문자열은 몇개의 문자로 이루어 졋느냐에 따라 필요한 메모리의 공간이 정해진다. <br>

그리하여 숫자 1은 1000000도 동일한 8바이트가 필요하지만 <br>
문자열의 경우 <br>
1개의 문자인 경우 -> 2바이트 <br>
20개의 문자인경우 -> 20바이트가 필요하다 <br>

c에서는 이러한 이유로 하나의 문자를 위한 데이터 타입(char)만 존재하며 문자열은 문자의 배열로 처리한다. <br>
java에서는 문자열을 string 객체로 처리한다 <br>

하지만 자바스크립트에서는 원시타입인 문자열 타입을 제공한다.

### 값에 의한 전달

```javascript
var test = 80;
var ttest = test;

test = 100;
console.log(test); //100
console.log(ttest); //80
```

변수에 변수를 할당했을때 무엇이 할당되는가? <br>
변수에 원시값을 할당하면 할당받는 변수에는 할당되는 변수의 원시값이 복사되어 전달된다 <br>
이를 <b>값에 의한 전달</b> 이라 칭한다 <br>

```javascript
var test = 80;
var ttest = test;
```

둘다 같은 80이라는 값을 가지자만 각각의 변수의 값은 다른 메모리 공간에저장된다 <br>

사실은 값에 의한 전달도 엄격하게 표현하면 값이 전달되는것이 아니라 메모리 주소를 전달한다. 단 전달된 메모리 주소를 통해 메모르 공간에 접근하면 값을 참조할수 있다. <br>
<b> 결론은 두 변수의 원시값은 서로 다른 메모리 공간에 저장된 별개의 값이 되어 어느 한쪽에서 재할당을 통해 값을 변경해도 서로 간섭할수 없다.</b>

### 자바스크립트의 객체 관리방식

자바스크립트 객체는 프로퍼티 키를 인덱스를 사용하는 해시 테이블과 유사하지만 높은 성능을 위해 더 나은 방법으로 객체를 구현한다.<br>

자바,c++의 같은 클래스 기반 객체지향 프로그래밍언어는 사전의 정의된 클래스를 기반으로 객체(인스턴스)를 생성한다. <br>
객체 생성 이전에 이미 프로퍼티와 메서드가 정해져 있으면 이를 따라서 객체를 생성한다. <br>

하지만 자바스크립트는 클래스없이 객체를 생성하며 생성후에도 프로퍼티와 메서드를 추가한다 사용은 편하지만 성능면에서는 클래스 기반 객체지향에 비해 생성과 프로퍼티 접근에 비용이 더많이 든다.<br>

이때문에 V8 자바스크립트 엔진에서는 동적탐색 대신 히든 클래스 방식을 사용하여 성능을 보장한다

### 객체 재할당

객체는 변경 가능한 값이다 <br>
객체를 할당한 변수가 기억하는 메모리 주소를 통해 메모리 공간에 접근하면 참조값에 접근 할수 있다 <br>
참조값은 생성된 객체가 저장된 메모리 공간의 주소 , 그자체이다
<br>
원시값을 가진 변수는 "변수가 ~~값을 가진다" 라 표현하지만 <br>
참조값을 가진 변수는 "변수가 객체를 가리킨다" 라 표현 한다<br>

메모리를 효율적으로 사용하기 위해 객체는 변경가능한 값으로 설정되어있는데 이러한 구조적 단점에 따른 부작용이 존재하는데 <br>
그것은 원시값과는 다르게 <b>여러개의 식별자가 하나의 객체를 공유할수도 있다는 것이다</b>

### 얕은복사 깊은복사

관점 1 <br>
객체를 프로퍼티값으로 가지는 객체의 경우 <br>

- 얕은 복사: 한단계 까지만 복사 <br>
- 깊은 복사: 객체에 중첩된 객체까지 전부 복사 <br>

하는것을 뜻한다

관점 2 <br>
변수에 값을 할당하는 경우 <br>

- 얕은 복사 : 객체에 할당한 변수를 다른변수에 할당하는것
- 깊은 복사 : 원시값을 할당한 변수를 다른변수에 할당하는것

```javascript
const v = 1;
const v1 = v; // v1 = 1 -> 깊은 복사

const o = { x: 1 };
const o2 = 0; // o = 1 -> 얕은 복사
```


#### reference

