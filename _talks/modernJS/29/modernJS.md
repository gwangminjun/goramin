---
title: "[모던 자바 스크립트] 29장 Math"
collection: talks
type: "Talk"
permalink: _talks/modernJS/29/modernJS
date: 2024-05-19
---

## 29장 Math

수학적인 상수와 함수를 위한 프로퍼티와 메서드 제공

### 프로퍼티

**Math.PI**

- 원주율 PI 값 제공.

### 메서드

**Math.round**

인수로 전달된 숫자의 소수점 이하를 반올림한 정수 반환.

```jsx
Math.round(1.4);  // -> 1
Math.round(1.6);  // -> 2
Math.round(-1.4); // -> -1
Math.round(-1.6); // -> -2
```

**Math.ceil**

인수로 전달된 숫자의 소수점 이하를 올림한 정수 반환.

```jsx
Math.ceil(1.4);  // -> 2
Math.ceil(1.6);  // -> 2
Math.ceil(-1.4); // -> -1
```

**Math.floor**

인수로 전달된 숫자의 소수점 이하를 내림한 정수 반환.

```jsx
Math.floor(1.9);  // -> 1
Math.floor(9.1);  // -> 9
Math.floor(-1.9); // -> -2
Math.floor(-9.1); // -> -10
Math.floor(1);    // -> 1
```

**Math.sqrt**

인수로 전달된 숫자의 제곱근 반환.

```jsx
Math.sqrt(9);  // -> 3
Math.sqrt(-9); // -> NaN
Math.sqrt(2);  // -> 1.414213562373095
Math.sqrt(1);  // -> 1
```

**Math.random**

임의의 난수를 반환.

```jsx
const random = Math.floor((Math.random() * 10) + 1);
console.log(random); // 1에서 10 범위의 정수
```

**Math.pow**

첫 번째 인수를 밑으로, 두 번째 인수를 지수로 거듭제곱하여 반환.

```jsx
Math.pow(2, 8);  // -> 256
Math.pow(2, -1); // -> 0.5
Math.pow(2);     // -> NaN

// ES7 지수 연산자
2 ** 2 ** 2; // -> 16
Math.pow(Math.pow(2, 2), 2); // -> 16
```

**Math.max**

전달받은 인수 중에서 가장 큰 수를 반환.

```jsx
Math.max(1); // -> 1
Math.max(1, 2); // -> 2
Math.max(1, 2, 3); // -> 3
Math.max(); // -> -Infinity
```

**Math.min**

전달받은 인수 중에서 가장 작은 수를 반환.

```jsx
Math.min(1); // -> 1
Math.min(1, 2); // -> 1
Math.min(1, 2, 3); // -> 1
Math.min(); // -> Infinity
```

#### reference

