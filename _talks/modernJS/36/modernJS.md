---
title: "[모던 자바 스크립트] 36장 디스트럭처링 할당"
collection: talks
type: "Talk"
permalink: _talks/modernJS/36/modernJS
date: 2024-06-02
---

# 36장 디스트럭처링 할당

---

# 디스트럭처링 할당
구조분해 할당이라고도 부른다.

구조화된 배열과 같은 **이터러블 또는 객체**를 **비구조화** 하여 **1개이상의 변수에 개별적으로 할당**하는것을 칭한다.

## 배열
### 기준
배열 디스트럭처링 할당의 대상은 **이터러블**이어야 하며

할당 기준은 **배열의 인덱스 순서**이다.

### 사용
```javascript
const arr = [1, 2, 3];
const [one, two, three] = arr; // 배열 디스트럭처링 할당
console.log(one, two, three); //1 2 3
```

배열 디스트럭처링 할당은 배열과 같은 이터러블에서 **필요한 요소만 추출하여 변수에 할당**하고 싶을때 유용하다

## 객체
### 기준
객체 디스트럭처링 할당의 대상은 **이터러블**이어야 하며

할당 기준은 **프로퍼티 키**다.

**즉 순서는 의미가없다.**

**선언된 변수이름과 프로퍼티 키가 일치하면 할당**된다.

### 사용
```javascript
const obj = { firstName : 'minjun' , lastName : 'yang'};

const { lastName, firstName} = obj;

console.log(firstName, lastName); //minjun yang

//기본값 설정
const { lastName = 'test', firstName} = obj; 
```



#### reference

