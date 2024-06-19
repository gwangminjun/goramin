---
title: "promiseAllSettled에 관하여"
collection: teaching
type: "js"
permalink: /teaching/promiseAllSettled/content
venue: "직장"
date: 2024-06-19
---

promiseAllSettled 에 관하여

## Promise.allSettled
Promise.allSettled는 전달된 모든 프로미스가 완료(fulfilled 또는 rejected)될 때까지 기다립니다. 
모든 프로미스가 완료된 후, 각 프로미스의 상태와 결과를 포함하는 객체 배열을 반환합니다.

## Promise.all 과의 차이
- Promise.allSettled: **모든 프로미스가 완료**될 때까지 기다립니다. 각 프로미스의 결과와 상태를 반환합니다.
- Promise.all: **모든 프로미스가 성공**할 때까지 기다립니다. 하나라도 실패하면 즉시 실패 이유를 반환하고 실행을 중단합니다.

## 사용
- Promise.allSettled는 여러 비동기 작업의 개별 결과를 모두 확인하고 처리해야 할 때
- Promise.all은 모든 비동기 작업이 성공해야만 할때

## 잘못된 사용

두 예제는 다른 동작 방식을 가진다

### 첫번째 예시
```js
const results = await Promise.allSettled([
    await getWeather(),
    await getWeatherWarning(),
]);
```
1. 함수들을 순차적으로 실행합니다.
2. getWeather()가 완료된 후 getWeatherWarning()가 실행됩니다.
3. 순차 실행합니다.
4. 병렬 실행의 이점을 활용하지 않습니다.

### 두번째 예시
```js
const results = await Promise.allSettled([
    getWeather(),
    getWeatherWarning(),
]);
```
1. 함수들을 병렬로 실행합니다.
2. getWeather()와 getWeatherWarning()가 동시에 실행되므로, 더 빠르게 완료될 수 있습니다.
3. 비동기 작업의 병렬 실행을 활용합니다.

- 병렬 실행과 순차 실행의 장단점을 고려하여 Promise.allSettled를 사용해야 함