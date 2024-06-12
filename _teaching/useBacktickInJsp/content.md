---
title: "jsp 안에서의 백틱"
collection: teaching
type: "java"
permalink: /teaching/useBacktickInJsp/content
venue: "직장"
date: 2024-06-12
---
JSP 안에서의 백틱(``) 사용

### 백틱(``)
JavaScript에서 백틱(``)을 사용하면 템플릿 리터럴(template literal)을 작성할 수 있다. <br> 
템플릿 리터럴은 문자열을 쉽게 생성하고, 여러 줄로 나눠 쓰거나, 변수와 표현식을 삽입할 수 있게 해주는 기능이다
```js
const title = "Welcome";
const body = "This is the body of the email.";
const html = `
  <html>
    <head><title>${title}</title></head>
    <body>
      <p>${body}</p>
    </body>
  </html>`;
console.log(html)
```
### jsp 속 script 에서의 백틱(``)
백틱(``)을 사용시 ${} 구문을 사용하여 변수와 표현식을 삽입하는데 <br>
이는 jsp 안의  **EL(Expression Language)** 로 해석될 수 있기 때문에 유의해야한다.

### EL
EL(Expression Language)은 JSP 페이지 내에서 데이터를 출력하고 변수를 조작하는 데 사용 <br>
EL은 주로 JSTL(JSP Standard Tag Library)과 자주 함께 사용된다.

### 해결법
1. JS 템플릿 리터럴 내의 ${} 구문을 문자열로 처리
```js
const $tr = $("<tr class='tCenter search_result' k='" + length + "'></tr>");
$tr.append("<td>" + gid + "</td>");
```
2. 백틱을 한번 더 감싸서 처리
```js
const $tr = $(`<tr class='tCenter search_result' k='${'${length}'}'></tr>`);
$tr.append(`<td>${'${gid}'}</td>`);
```
둘 중 편한 방법을 사용하면 된다.