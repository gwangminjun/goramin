---
title: "mybatis Type Exception 에러"
collection: teaching
type: "mybatis"
permalink: /teaching/mybatisTypeException/content
venue: "직장"
date: 2024-06-12
---
mybatis Type Exception 오류

  
![img_4.png](img_4.png)
## Type Exception 오류시 해결
mybatis xml 파일 작성시 parameterType , resultType 설정 확인
### 1. 전체 vo 경로 작성
   - ![img_5.png](img_5.png)

### 2. mybatis config 설정파일에 typeAlias 추가
   - ![img_3.png](img_3.png)
   
둘 중 편한대로 하면 된다.