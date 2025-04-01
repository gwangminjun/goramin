---
title: "[모던 자바 스크립트] 30장 Date"
collection: talks
type: "Talk"
permalink: _talks/modernJS/30/modernJS
date: 2024-05-19
---

# 30장 Date

---
Date 는 날짜와 시간(연, 월, 일, 시, 분, 초, 밀리초)을 위한 메서드를 제공하는

빌트인 객체이면서 생성자 함수이다.

### UTC

UTC는 국제 표준시를 의미한다.

기술적인 표기에서는 UTC가 사용된다.

KST(한국 표준시)는 UTC에 9시간을 더한 시간이다.

즉, KST는 UTC보다 9시간이 빠르다.

### 메서드

**Date.prototype.toDateString**

사람이 읽을 수 있는 형식의 문자열로 Date 객체의 날짜를 반환한다.

```
const today = new Date("2020/7/24/12:30");
today.toString(); // -> Fri Jul 24 2020 12:30:00 GMT+0900 (한국 표준시)
today.toDateString(); // -> Fri Jul 24 2020
```

**Date.prototype.toLocalString**

인수로 전달한 **로컬을 기준** 으로 하는 **Date 객체의 날짜와 시간을 표현한 문자열을 반환** 메서드!

**인수를 생략한 경우 브라우저가 동작 중인 시스템의 로컬을 적용한다**

```
const today = new Date("2020/7/24/12: 30");

today.toString(); // ->  Fri Jul 24 2020 12:30:00 GMT+0900 (한국 표준시)
today.toLocaleString(); // -> 2020. 7. 24. 오후 12:30:00
today.toLocaleString("ko-KR"); // -> 2020. 7. 24. 오후 12:30:00
today.toLocaleString("en-US"); // -> 7/24/2020, 12:30:00 PM
today.toLocaleString("ja-JP"); // -> 2020/7/24 12:30:00
```

**Date.prototype.toLocaleTimeString**

인수로 전달한 **로컬을 기준** 으로 하는 **Date 객체의 시간을 표현한 문자열을 반환** 메서드!

**인수를 생략한 경우 브라우저가 동작 중인 시스템의 로컬을 적용한다**

```
const today = new Date("2020/7/24/12: 30");

console.log(today.toString()); // -> Fri Jul 24 2020 12:30:00 GMT+0900 (한국 표준시)
console.log(today.toLocaleTimeString()); // -> 오후 12:30:00
console.log(today.toLocaleTimeString("ko-KR")); // -> 오후 12:30:00
console.log(today.toLocaleTimeString("en-US")); // -> 12:30:00 PM
console.log(today.toLocaleTimeString("ja-JP")); // -> 12:30:00
```

#### reference

