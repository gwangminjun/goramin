---
title: "[우아한 타입스크립트 with 리액트] 3장 고급타입"
collection: talks
type: "Talk"
permalink: _talks/woowahanTS/3/content
date: 2024-08-25
---

## 3장 고급타입

## 이슈
### 3.3.6. 제네릭의 장점을 살려 사용할 수 있는 작성 케이스로는 무엇이 있을까요?  (115~118p)

# JSON 데이터 , XML 데이터 파싱

JSON 과 XML 데이터를 타입 상관없이 받아서
파싱 핸들러 함수를 통합 처리

```ts

import { parseStringPromise } from 'xml2js';

//데이터 타입 선언
enum DataType {
    JSON = 'json',
    XML = 'xml'
}

// 파싱 핸들러 함수
async function parseData<T>(data: string, dataType: DataType): Promise<T> {
    if (dataType === DataType.JSON) {
        return JSON.parse(data) as T;
    } else if (dataType === DataType.XML) {
        const result = await parseStringPromise(data);
        return result as T;
    } else {
        throw new Error("Unsupported data type");
    }
}


// JSON 데이터 예시
const jsonData = `{
    "name": "minjun",
    "age": 28
}`;

// XML 데이터 예시
const xmlData = `
<Person>
    <name>minjun</name>
    <age>28</age>
</Person>
`;

// JSON 데이터 타입
interface PersonJSON {
    name: string;
    age: number;
}

// XML 데이터 타입
// XML은 구조상 동일한 데이터가 들어갈수있기때문에 배열로 처리한다
interface PersonXML {
    Person: {
        name: string[];
        age: string[];
    };
}

// JSON 데이터 파싱
parseData<PersonJSON>(jsonData, DataType.JSON).then(personFromJSON => {
    console.log(personFromJSON.name); // "John"
    console.log(personFromJSON.age);  // 30
});

// XML 데이터 파싱
parseData<PersonXML>(xmlData, DataType.XML).then(personFromXML => {
    console.log(personFromXML.Person.name[0]); // "John"
    console.log(personFromXML.Person.age[0]);  // "30"
});

```

=============================================================

### 3.2.6 특정 문자가 들어간 타입을 만들어 보세요! (105p)

규칙

1. 제네릭과 템플릿 리터럴 타입을 사용해서 자유롭게 구현해주세요.
2. 'ing' 접미사를 가진 단어만 허용하는 타입을 만들어주세요.
3. 새로 생성할 타입의 이름은 'EndAndIng로 해주세요.


```ts
// 선언
type EndAndIng<T extends string> = T extends `${string}ing` ? T : never;

// 올바른 사용
type Searching = EndAndIng<'Searching'>; // 'Searching'
type Studying = EndAndIng<'Studying'>; // 'Studying'

// 오류
type Search = EndAndIng<'Search'>; // never
type Study = EndAndIng<'Study'>;   // never

// 제네릭 함수와 함께 사용 예시
function useIngWord<T extends string>(word: EndAndIng<T>): T {
    
    if (word === (undefined as never)) {
        throw new Error("The word must end with 'ing'.");
    }
    return word;
}

try {
    const validWord = useIngWord('Swimming'); // 정상 작동
    console.log(validWord); // 출력: Swimming
} catch (error) {
    console.error((error as Error).message);
}

try {
    const invalidWord = useIngWord('Swim'); // 컴파일 타임 에러 발생
    console.log(invalidWord);
} catch (error) {
    console.error((error as Error).message); // 추후에 swim 이 아닌 입력값으로 검증해야 할때 런타임 에러 발생을 위해 추가
}

```

=============================================================

### 3.3.4 제한된 제네릭을 사용하는 경우와 예시를 들어 설명해주세요. ( p112~p113)

## 예시

```ts
interface Minjun {
    name: string;
    pair: string;
}

// pair가 string 또는 null일 수 있으므로 반환 타입을 string | null로 설정
function getPair<T extends Minjun>(obj: T): string {
    return obj.pair;
}}

// 올바른 상황
const LoveMinjun = { name: '양민준', pair: '박규영' };
console.log(getPair(LoveMinjun)); // 출력: 박규영

// 현재 상황
const CurrentMinjun = { name: '양민준', pair: null };

// 오류 발생 : NULL
```

=============================================================

### 3.1.5 옵셔널 프로퍼티를 사용해야 하는 상황 (94p)

# 옵셔널 프로퍼티

## 사용

객체의 속성이 선택적일때 사용한다

```ts

interface User {
    name: string;
    habbit?: string; // age는 선택적 프로퍼티입니다.
}

const user1: User = {
    name: "minjun",
    habbit: "study"
};

const user2: User = {
    name: "Bob"
};

```

## 주의사항
### undefined 처리

옵셔널 프로퍼티는 정의 되지 않을수있기 때문에 기본값을 정의하지 않는경우 undefined 값 처리시 문제가 발생한다

객체 구조 할당 처리 예시
```ts
interface UserSettings {
    theme?: string;
    notifications?: boolean;
}

function applySettings(settings: UserSettings) {
    const { theme, notifications } = settings;
    console.log(`Theme: ${theme}`);
    console.log(`Notifications: ${notifications}`);
}

//객체 구조 할당
//const userSettings: UserSettings = { theme: 'dark' };

// 출력: Theme: dark
// 출력: Notifications: undefined 
//(기본값이 없으므로, notifications가 undefined일 때 처리되지 않음)
applySettings(userSettings);
```

=============================================================

### 3.3.5 맵드 타입의 readonly 수식어의 사용 (p102)

### readonly 수식어를 사용해야 하는 상황
1. 객체의 불변성(immutability)을 유지
   ```ts
   type AppSettings = {
        readonly theme: string;
        readonly version: string;
        readonly isBeta: boolean;
   };

    // AppSettings 타입의 객체 생성
    const settings: AppSettings = {
        theme: "dark",
        version: "1.0.0",
        isBeta: false,
    }; 

    // 수정 시도 시 컴파일 에러 발생
    settings.theme = "light" // Error 
   ```
2. 데이터의 무결성을 보장
    ```ts
    type UserProfile = {
        readonly id: number;
        readonly name: string;
        readonly email: string;
    };

    const user: UserProfile = {
        id: 1,
        name: "minjun",
        email: "minjun@example.com",
    };

    // 수정 시도 시 컴파일 에러 발생
    // user.name = "Jane Doe"; // Error

    ```

3. 옵셔널과의 혼합 사용예시
   ```ts
    type BasicProfile = {
        username: string;
        age: number;
    };

    const profile1: BasicProfile = {
        username: "minjun", // age는 선택적
        age: 28;
    };

    // age를 옵셔널로 변환
    type ProfileWithOptionalAge = {
        username: string;
        age?: number;
    };

    const profile2: ProfileWithOptionalAge = {
        username: "minjun", // age는 선택적
    };

    // 맵드 타입을 사용해 모든 속성을 선택적으로 변환
    type OptionalProfile = {
        [K in keyof BasicProfile]?: BasicProfile[K];
    };

    const profile3: OptionalProfile = {
        username: "minjun", // 모든 속성은 선택적
    };

    const profile4: OptionalProfile = {}; // 모든 속성을 생략할 수 있음

   ```

=============================================================
