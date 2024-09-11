---
title: "[우아한 타입스크립트 with 리액트] 1장 들어가며"
collection: talks
type: "Talk"
permalink: _talks/woowahanTS/0/content
date: 2024-03-02
---

# 1장 들어가며

## 이슈

1. 1.1.4  CBD(Component Based Development) 방법론은 어떻게 등장하게 되었고, 해당 방식의 장점에는 어떤 것들이 있을까요?
   
   - 답변:
   ![img.png](img.png)
      참조 <br>
      https://velog.io/@ainochi95/20m-CBDComponent-Based-Development <br>
      https://blog.naver.com/jvioonpe/220246549818 <br>
   
2. 1.2.3_PropTypes 과 TypeScript 의 차이와 TypeScript를 사용해야하는 이유는 무엇일까요?

   - 답변:
   # PropTypes 과 TypeScript 의 차이

    ## PropTypes
    React의 props에 대한 "런타임 유형 검사 도구"
    컴포넌트에서 예상되는 props 유형을 정의
    
    ### PropTypes 의 오류
    PropTypes 는 프로덕션 응용 프로그램(vscode)에서 경고를 따로 제공하지 않으며 경고는 "개발 중에만" 표시
    
    개발자 모드에서 직접 실행해보기 전(npm start)까지는 코드를 작성하면서는 해당 오류를 바로 캐치할 수 없음
    
    ## TypeScript
    React와 함께 TypeScript 를 사용하면 컴파일할 때 확인할 내용을 props에 추가할 수 있다.
    
    ### TypeScript 의 오류
    예기치 않은 props 를 전달할 때 vscode(IDE)에 즉각적인 IntelliSense 경고가 표시
    코드를 작성하는 순간순간 오류를 바로 캐치
    
    TypeScript 를 사용하면 다음과 같이 props 요구 사항을 위반할 시 npm run build를 실행할 수 없다.

    ## TypeScript 와 PropTypes 비교
    ### 런타임 및 컴파일 시간 유형 확인
   - PropTypes : 브라우저에서 실행되는 동안 런타임 중에 유형 검사를 수행
   - TypeScript : 컴파일될 때 컴파일 시간 동안 유형 검사를 수행
    ### 구문 및 의미 강조
   - TypeScript 강조 표시 도구는 PropTypes를 능가한다 (IDE 제공)
   - TypeScript 예상되는 props의 데이터 유형이 제공되지 않을 때 구성 요소를 적절하게 강조 표시하고 솔루션에 대한 통찰력을 제공
    ## TypeScript 고급 기능
    ### 조건부 유형 검사
    - 속성 A가 true인 경우 속성 C도 제공해야 한다


참조
- https://velog.io/@serenity/React-TypeScript-vs-PropTypes
 

