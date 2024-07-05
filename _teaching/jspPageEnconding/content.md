---
title: "jspPageDirective 에 대해서"
collection: teaching
type: "jsp"
permalink: /teaching/jspPageDirective/content
venue: "직장"
date: 2024-07-05
---
jsp PageEnconding 에 대해서

### 상황
html 파일을 jsp 파일로 변경하는 중에 
```html
<meta charset="UTF-8">
```
jspPageDirective 에 대해서

### jspPageDirective
JSP (JavaServer Pages)에서 Page Directive는 JSP 페이지의 설정과 환경을 정의하는데 사용됩니다. 
Page Directive는 <%@ page ... %> 형식으로 사용되며, 여러 속성을 통해 JSP 페이지의 동작을 제어할 수 있습니다.

**page에 대한 속성을 부여**

### 속성
1. import
- JSP 페이지에서 사용할 Java 클래스를 지정
- Java의 import 구문과 비슷
```jsp
<%@ page import="java.util.List, java.util.ArrayList" %>
```
2. contentType
- JSP 페이지가 생성하는 응답의 MIME 타입을 설정합니다. 
- 기본값은 text/html; charset=ISO-8859-1입니다.
```jsp
<%@ page contentType="text/html; charset=UTF-8" %>
```
3. pageEncoding
- JSP 페이지 파일의 문자 인코딩을 지정합니다.
```jsp
<%@ page pageEncoding="UTF-8" %>
```
4. session
- 현재 페이지에서 세션을 사용할지 여부를 지정합니다. 
- 기본값은 true입니다.
```jsp
<%@ page session="false" %>
```
5. buffer
- JSP 페이지의 출력 버퍼 크기를 설정합니다. 
- 기본값은 8kb입니다.
```jsp
<%@ page buffer="16kb" %>
```
6. autoFlush
- 출력 버퍼가 가득 찼을 때 자동으로 비울지 여부를 지정합니다. 
- 기본값은 true입니다.
```jsp
<%@ page autoFlush="false" %>
```

7. isThreadSafe
- JSP 페이지가 스레드 안전한지 여부를 지정합니다. 
- 기본값은 true입니다.
```jsp
<%@ page isThreadSafe="false" %>
```
8. errorPage
- 오류가 발생했을 때 이동할 페이지를 지정합니다.
```jsp
<%@ page errorPage="error.jsp" %>
```
9. isErrorPage
- 현재 페이지가 오류 페이지인지 여부를 지정합니다. 
- 기본값은 false입니다.
```jsp
<%@ page isErrorPage="true" %>
```
10. language
- JSP 페이지가 사용할 스크립팅 언어를 지정합니다. 
- 기본값은 java입니다.
```jsp
<%@ page language="java" %>
```
11. extends
- JSP 페이지가 상속할 클래스를 지정합니다.
```jsp
<%@ page extends="com.example.MyBaseClass" %>
```
12. info
- JSP 페이지에 대한 설명 정보를 설정합니다.
```jsp
<%@ page info="This is a sample JSP page" %>
```
13. isELIgnored
- Expression Language (EL)를 무시할지 여부를 지정합니다. 
- 기본값은 false입니다.
```jsp
<%@ page isELIgnored="true" %>
```


### 실제 사용한 모습
```jsp
<%@ page language="java" contentType="text/html" pageEncoding="UTF-8" %>
```

상황에 맞춰 사용하면 된다.
## 참조
- https://m.blog.naver.com/ka28/221996368625