---
title: "jsp PageEnconding 에 대해서"
collection: teaching
type: "encode"
permalink: /teaching/jspPageEnconding/content
venue: "직장"
date: 2024-07-05
---
jsp PageEnconding 에 대해서

### 상황
html 파일을 jsp 파일로 변경하는 중에 
```html
<meta charset="UTF-8">
```
지정함에도 파일이 인코딩이 에러가 났엇다

### charset과 pageencoding의 차이
- charset 
  - JSP 페이지가 생성하는 응답의 MIME 타입과 문자 인코딩을 설정하는 데 사용됩니다.
- pageEncoding
  - JSP 페이지 자체의 문자 인코딩을 지정하는 데 사용됩니다. 
  - 이는 JSP 파일이 어떤 인코딩으로 작성되었는지 JSP 컨테이너에게 알려줍니다.
- 목적
  - charset: 클라이언트에게 응답의 문자 인코딩을 알리기 위해 사용됩니다.
  - pageEncoding: JSP 파일 자체의 문자 인코딩을 지정하기 위해 사용됩니다.
- 적용
  - charset: 브라우저가 응답을 해석하는 방식에 영향을 미칩니다.
  - pageEncoding: JSP 컨테이너가 JSP 파일을 해석하고 컴파일하는 방식에 영향을 미칩니다.

### pageencoding 적용
page directve로 적용 하여 해결하였다.

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
```
## 참조
- https://m.blog.naver.com/alcmskfl17/221913121686
- https://webie.tistory.com/169
- https://m.blog.naver.com/ka28/221996368625