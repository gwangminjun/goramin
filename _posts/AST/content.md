---
title: 'AST 에 대하여'
date: 2024-06-12
permalink: _posts/AST/content
tags:
  - javascript
  - compiler
  - Transpiler
  - Tech
---
### 서문
주말마다 하는 모던 자바스크립트 책 스터디가 있는데 AST 내용이 언급되었다.<br>
해당 개념에대한 설명을 하려는데 스스로 해당 개념에대한 이해가 떨어지는 것을 느껴서 해당 포스팅을 작성한다.

자바스크립트를 깊이 이해하기 위해서는 코드를 단순히 작성하고 실행하는 것을 넘어서, <br> 
내부적으로 어떻게 동작하는지 이해하는 것이 중요하다. <br>
그 중에서도 추상 구문 트리(Abstract Syntax Tree, AST)는 컴파일러나 인터프리터가 소스 코드를 처리하는 데 필수적인 개념입니다.<br> 
이번 포스팅에서는 AST의 개념과 역할, 그리고 자바스크립트에서의 활용에 대해 살펴보겠습니다. +) with Babylon,babel

### 참조
- [https://itnext.io/ast-for-javascript-developers-3e79aeb08343](https://openai.com/index/gpt-4/)
- [https://www.sitepoint.com/understanding-asts-building-babel-plugin/](https://openai.com/index/gpt-4/)
- [https://dev.to/this-is-learning/what-is-babel-and-swc-49cp](https://openai.com/index/gpt-4/)
- [https://gyujincho.github.io/2018-06-19/AST-for-JS-devlopers](https://openai.com/index/gpt-4/)
- [https://openai.com/index/gpt-4/](https://openai.com/index/gpt-4/)