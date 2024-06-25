---
title: "[모던 자바 스크립트] 37장 set/map"
collection: talks
type: "Talk"
permalink: _talks/modernJS/37/modernJS
date: 2024-06-09
---

## 37장 set/map

# Set
Set 객체는 중복되지 않는 유일한 값들의 집합
![img.png](img.png)

## set 객체의 생성
- set 생성자 함수로 생성, 인수를 전달하지 않으면 set 객체 생성
```javascript
const set = new Set();
```

## set 요소 개수 확인
- Set 객체의 요소 개수를 확인할 때는 Set.prototype.size 프로퍼티를 사용한다.
```javascript
const { size } = new Set([2, 1, 3, 3]);
console.log(size); // 3
```
- size 프로퍼티는 setter 함수 없이 getter 함수만 존재하는 접근자 프로퍼티다.
- 따라서 size 프로퍼티에 숫자를 할당하여 Set 객체의 요소 개수를 변경할 수 없다.

## set 요소 추가
- Set 객체에 요소를 추가할 때는 Set.prototype.add 메서드를 사용한다.
```javascript
const set = new Set();
console.log(set); // Set(0) {}

set.add(1);
console.log(set); // Set(1) {1}
```

## set 요소 존재 여부 확인
- Set 객체에 특정 요소가 존재하는지 확인하려면 Set.prototype.has 메서드를 사용한다.
```javascript
const set = new Set([1, 2, 3]);

console.log(set.has(2)); // true
console.log(set.has(4)); // false
```
## set 요소 삭제
- Set 객체에 특정 요소를 삭제하려면 Set.prototype.delete 메서드를 사용한다.
```javascript
const set = new Set([1, 2, 3]);

// 요소 2 삭제
set.delete(2);
console.log(set); // Set(2) { 1, 3 }
```

## set 요소 일괄 삭제
- Set 객체에 모든 요소를 일괄 삭제하려면 Set.prototype.clear 메서드를 사용한다.
```js
const set = new Set([1, 2, 3]);

set.clear();
console.log(set); // Set(0) {}
```

## set 요소 순회
- Set 객체에 요소를 일괄 순회하려면 Set.prototype.forEach 메서드를 사용한다.
```javascript
const set = new Set([1, 2, 3]);

set.forEach((v, v2, set) => console.log(v, v2, set));
/*
1 1 Set(3) {1, 2, 3}
2 2 Set(3) {1, 2, 3}
3 3 Set(3) {1, 2, 3}
*/
```
- Set 객체는 **이터러블이다**.
- 따라서 for...of 문으로 순회할 수 있으며, 스프레드 문법과 배열 디스트럭처링의 대상이 될 수 도 있다.
```javascript
const set = new Set([1, 2, 3]);

// for...of 문
for (const value of set) {
    console.log(value); // 1 2 3
}

// 스프레드 문법
console.log([...set]); // [1, 2, 3]

// 배열 디스트럭처링
const [a, ...rest] = set;
console.log(a, rest); // 1 [2, 3]
```

## 집합 연산
### 교집합
- 집합 A와 집합 B의 공통 요소로 구성한다.
```javascript
Set.prototype.intersection = function(set) {
    const result = new Set();

    for (const value of set) {
        // 2개의 set의 요소가 공통되는 요소이면 교집합의 대상이다.
        if (this.has(value)) {
            result.add(value);
        }
    }

    return result;
}

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

//setA와 setB의 교집합
console.log(setA.intersection(setB)); // Set(2) { 2, 4 }
//setB와 setA의 교집합
console.log(setB.intersection(setA)); // Set(2) { 2, 4 }
```
### 합집합
- 집합 A와 집합 B의 중복 없는 모든 요소로 구성된다.
```javascript
Set.prototype.union = function(set) {
    // this(Set 객체 복사)
    const result = new Set(this);

    for (const value of set) {
        // 합집합은 2개의 Set 객체의 모든 요소로 구성된 집합니다. 중복된 요소는 포함되지 않는다.
        result.add(value);
    }

    return result;
}

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

//setA와 setB의 합집합
console.log(setA.union(setB)); // Set(4) { 1, 2, 3, 4 }
//setB와 setA의 합집합
console.log(setB.union(setA)); // Set(4) { 2, 4, 1, 3 }
```
### 차집합
- 집합 A에는 존재하지만 집합 B에는 존재하지 않는 요소로 구성된다.
```javascript
Set.prototype.difference = function(set) {
    // this(Set 객체)를 복사
    const result = new Set(this);

    for (const value of set) {
        // 차집합은 어느 한쪽 집합에는 존재하지만 다른 한쪽 집합에는 존재하지 않는 요소로 구성한 집합이다.
        result.delete(value);
    }

    return result;
}

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

//setA에 대한 setB의 차집합
console.log(setA.difference(setB)); // Set(2) {1, 3}
//setB에 대한 setA의 차집합
console.log(setB.difference(setA)); // Set(0) {}
```
### 부분집합과 상위 집합
```javascript
// this가 subset의 상위 집합인지 확인한다. 
Set.prototype.isSuperset = function(subset) {
    for (const value of subset) {
        // superset의 모든 요소가 subset의 모든 요소를 포함하는지 확인
        if (!this.has(value)) {
            return false;
        }
    }
    return true;
}

const setA = new Set([1, 2, 3, 4]);
const setB = new Set([2, 4]);

// setA가 setB의 상위 집합인지 확인한다.
console.log(setA.isSuperset(setB)); // true
// setB가 setA의 상위 집합인지 확인한다.
console.log(setB.isSuperset(setA)); // false
```


# Map
- Map 객체는 키와 값의 쌍으로 이루어진 컬렉션이다.
  ![img_1.png](img_1.png)

## Map 객체 생성
- Map 객체는 Map 생성자 함수로 생성한다.
```javascript
const map = new Map();
console.log(map); // Map(0) {}
```

## Map 요소 개수 확인
- Map 객체의 요소 개수를 확인할 때는 Map.prototype.size 프로퍼티를 사용한다.
```javascript
const { size } = new Map([['key1', 'value1'], ['key2', 'value2']]);
console.log(size); // 2
```

## Map 요소 추가
- Map 객체에 요소를 추가할 때는 Map.prototype.set 메서드를 사용한다.
```javascript
const map = new Map();
console.log(map); // Map(0) {}

map.set('key1', 'value1');

console.log(map) // Map(1) { 'key1' => 'value1' }
```
- 객체와의 차이는 객체는 **문자열 또는 심벌값** 만 키로 사용 가능하다
- Map 객체는 키타입에 제한이 없으므로 **객체를 포함한 모든값**을 키로 사용할수 있다
```javascript
const map = new Map();

const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

// 객체도 키로 사용할 수 있다.
map
    .set(lee, 'developer')
    .set(kim, 'designer');

console.log(map);
// Map(2) { { name: 'Lee' } => 'developer', { name: 'Kim' } => 'designer'}
```
## Map 요소 취득
- Map 객체에서 특정 요소를 취득하려면 Map.prototype.get 메서드를 사용한다.
```javascript
const map = new Map();

const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

map
    .set(lee, 'developer')
    .set(kim, 'designer');

console.log(map.get(lee)); // developer
console.log(map.get('key')); // undefined
```

## Map 요소 존재 여부 확인
- Map 객체에서 특정 요소가 존재하는지 확인하려면 Map.prototype.has 메서드를 사용한다.
```javascript
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

console.log(map.has(lee)); // true
console.log(map.has('key')); // false
```

## Map 요소 삭제
- Map 객체에서 요소를 삭제하려면 Map.prototype.delete 메서드를 사용한다.
```javascript
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

map.delete(kim);
console.log(map); // Map(1) { { name: 'Lee' } => 'designer' }
```

## Map 요소 일괄 삭제
- Map 객체에서 요소를 일괄 삭제하려면 Map.prototype.clear 메서드를 사용한다.
```javascript
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

map.clear();
console.log(map); // Map(0) {}
```

## Map 요소 순회
- Map 객체에 요소를 일괄 순회하려면 Map.prototype.forEach 메서드를 사용한다.
```javascript
const lee = { name: 'Lee' };
const kim = { name: 'Kim' };

const map = new Map([[lee, 'developer'], [kim, 'designer']]);

map.forEach((v, k, map) => console.log(v, k, map));
/*
    developer { name: 'Lee' } Map(2) {
      { name: 'Lee' } => 'developer',
      { name: 'Kim' } => 'designer'
    }
    designer { name: 'Kim' } Map(2) {
      { name: 'Lee' } => 'developer',
      { name: 'Kim' } => 'designer'
    }
*/
```
- Map 객체 또한 **이터러블**이다

## Map 객체와 일반객체의 차이점
1. The construction is of course different
   ( 구조적인 차이 )
    ```js
    const gamesObj = { 
        1: '시타델',
        2: '촐킨'   
    };
    
   const gamesMap = new Map([ 
        [1, 'Citadels'],
        [2, 'Tzolkin']
    ]);
    ```
2. Keys on objects are strings, on maps keys are of any type
   ( 객체의 키값은 문자열, 맵의 키는 모든 데이터 타입이 된다. )
    ```js
    console.log(gamesObj[1]);
    console.log(gamesObj['1']);
    
    console.log(gamesMap.get(1)); 
    console.log(gamesMap.get('1'));
    ```
3. Object maps inherit unwanted keys from the prototype
   (  맵 객체는 프로토타입으로부터 원치 않는 키를 상속 받는다. )
    ```js
    console.log(Object.prototype);
    const mapObject = {};
    console.log(mapObject['toString']);
    //ƒ toString() { [native code] }
    const mapObject = Object.create(null);
    console.log(mapObject['toString']);
    //undefined
    ```
4. Maps preserve the order of their keys, objects do not
   (  키 값의 순서 보존하고, 객체는 순서가 없다. )
    ```js
    const gamesObj = {
        2: 'Tzolkin',
        1: 'Citadels',
    };
    const keys = Object.keys(gamesObj);
    console.log(keys);
    //["1", "2"];
    const keyValuePairs = Object.entries(gamesObj);
    console.log(keyValuePairs);
    //["1", "Citadels"]
    //["2", "Tzolkin"]
   
   const gamesMap = new Map([
        [2, 'Tzolkin'],
        [1, 'Citadels']
    ])
    const keys = gamesMap.keys();
    console.log(keys);
    //MapIterator {2, 1}
    const keyValuePairs = gamesMap.entries();
    console.log(keyValuePairs);
    //MapIterator {2 => "Tzolkin", 1 => "Citadels"}
    ```
5. Maps offer a nicer interface for accessing entries
   ( 엔트리 접근하기 위한 훨씬 인터페이스가  좋다. )
    ```js
    const gamesObj = {
        2: 'Tzolkin',
        1: 'Citadels',
    };
    //값 접근시
    //1
    gamesObj[1];
    //'Citadels'
   
    //2
    const anotherGamesObj = {
    id1: 'Citadels',
    id2: 'Tzolkin'  
    };
    console.log(anotherGamesObj.id1);
    //'Citadels'
   
    //3
    gamesMap.get(1);
    //'Citadels'
    
    // 키의 존재 확인
    gamesMap.has(1);
    //true
    gamesMap.get(3);
    //false
    ```
6. Objects require helpers functions for accessing the key-values pairs
   ( 객체는 key-values 쌍에 접근하기 위한 보조 함수가 필요하다. )
    ```js
    const gamesMap = new Map([
        [1, 'Citadels'],
        [2, 'Tzolkin']
    ]);
    gamesMap.forEach((value, key)=>{
    console.log(`${key} - ${value}`)
    });
    //1 - Citadels
    //2 - Tzolkin
   
    //객체인경우 Object.entries를 사용해야함
    const gamesObj = {
        1: 'Citadels',
        2: 'Tzolkin'  
    };
    Object
    .entries(gamesObj)
    .forEach(([key, value])=>{
    console.log(`${key} - ${value}`)
    });
    //1 - Citadels
    //2 - Tzolkin
    ```
7. JSON offers support for objects but not for maps
   ( JSON은 객체를 지원하지만 맵은 안함 )
    ```js
    const gamesMap = new Map([
        [1, 'Citadels'],
        [2, 'Tzolkin']
    ]);
    const json = JSON.stringify(gamesMap);
    console.log(json);
    //{}
    ```
   
#### reference
- https://velog.io/@jjinichoi/%EB%AA%A8%EB%8D%98-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-Set%EA%B3%BC-Map
- https://medium.com/dailyjs/7-differences-between-objects-and-maps-in-javascript-bc901dfa9350
- https://velog.io/@jjinichoi/%EB%AA%A8%EB%8D%98-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-Deep-Dive-Set%EA%B3%BC-Map




