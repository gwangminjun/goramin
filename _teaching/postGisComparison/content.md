---
title: "postgis 객체 비교 함수"
collection: teaching
type: "PostGis"
permalink: /teaching/postGisComparison/content
venue: "직장"
date: 2024-06-13
---
postGis 함수를 사용하여 geometry 객체 비교 할일이 생겼다

### 종류
### 1. ST_Contains 
   **특징**: 하나의 지오메트리가 다른 지오메트리를 **완전히 포함**할 때 참을 반환합니다.<br>
   **사용**: ST_Contains(geomA, geomB)는 geomA가 geomB를 완전히 포함할 때 참을 반환합니다. <br>
   **예시**: 만약 geomA가 폴리곤이고 geomB가 이 폴리곤 내부의 포인트라면 참을 반환합니다. <br>
### 2. ST_DWithin
   **특징**: 두 지오메트리가 **지정된 거리 이내**에 있을 때 참을 반환합니다.<br>
   **사용**: ST_DWithin(geomA, geomB, distance)는 geomA와 geomB가 distance 거리 이내에 있을 때 참을 반환합니다.<br>
   **예시**: 만약 geomA가 포인트이고 geomB가 다른 포인트인데, 이 두 포인트가 100 미터 이내에 있다면 참을 반환합니다.<br>
### 3. ST_Equals
   **특징**: 두 지오메트리가 **동일한 형태와 위치**를 가질 때 참을 반환합니다.<br>
   **사용**: ST_Equals(geomA, geomB)는 geomA와 geomB가 동일한 지오메트리일 때 참을 반환합니다.<br>
   **예시**: 만약 두 폴리곤이 동일한 꼭지점과 형태를 가지고 있으면 참을 반환합니다.<br>
### 4. ST_Intersects
   **특징**: 두 지오메트리가 **한 점이라도 겹칠 때** 참을 반환합니다.<br>
   **사용**: ST_Intersects(geomA, geomB)는 geomA와 geomB가 교차할 때 참을 반환합니다.<br>
   **예시**: 만약 두 라인이 한 점에서 교차하면 참을 반환합니다.<br>
### 5. ST_Envelope
   **특징**: 지오메트리의 **최소 경계 박스**를 반환합니다.<br>
   **사용**: ST_Envelope(geom)는 geom의 최소 경계 박스를 반환합니다.<br>
   **예시**: 만약 geom이 복잡한 폴리곤이면, 그 폴리곤을 완전히 포함하는 직사각형을 반환합니다.<br>
### 6. ST_Within
   **특징**: 하나의 지오메트리가 **다른 지오메트리 내부**에 있을 때 참을 반환합니다.<br>
   **사용**: ST_Within(geomA, geomB)는 geomA가 geomB 내부에 있을 때 참을 반환합니다.<br>
   **예시**: 만약 geomA가 포인트이고 geomB가 폴리곤인데, 포인트가 폴리곤 내부에 있다면 참을 반환합니다.<br>
   
### 요약
- **ST_Contains**: A가 B를 완전히 포함하는지 확인합니다.<br>
- **ST_DWithin**: A와 B가 지정된 거리 이내에 있는지 확인합니다.<br>
- **ST_Equals**: A와 B가 동일한지 확인합니다.<br>
- **ST_Intersects**: A와 B가 교차하는지 확인합니다.<br>
- **ST_Envelope**: A의 최소 경계 박스를 반환합니다.<br>
- **ST_Within**: A가 B 내부에 있는지 확인합니다.<br>

상황에 맞춰 사용하면 된다.