---
title: "postgres 레이어 편집"
collection: teaching
type: "PostGis"
permalink: /teaching/postgresLayerEdit/content
venue: "직장"
date: 2024-08-06
---
전국 기준 레이어 데이터를 원하는 지역 레이어로 편집하기

### 요구사항
https://its.go.kr/opendata/opendataList?service=nodelink <br>
its 에서 획득한 표준 노드 링크 정보를 원하는 지역으로 자르기

### 해결방법
#### 전제
1. 기준데이터의 존재 유무
   - 전국 데이터 와 비교할 기준 데이터가 존재하는지
   - 없는 경우 qgis 클립핑으로 그려서 하는 방법 외엔 모른다.
   - 다만 직접 그리는 경우 데이터의 신뢰성을 보장할수 없으므로 비추

2. 존재할 경우
   1. QGIS 클립핑 사용 (https://wikidocs.net/166160)
   - 단점은 Qgis 사용에 대해 익숙해야함

   2. postgis 공간 함수 사용
   - 단점은 굉장히 오래 걸린다
     ```postgresql
       INSERT INTO xeus.its_link_ls 
       SELECT
       ST_Transform(ST_SetSRID(ml._geometry, 5186), 4326) AS _geometry
       FROM xeus."MOCT_LINK" ml
       JOIN xeus.kais_emd_as emd ON ST_Intersects(
       ST_Transform(ST_SetSRID(ml._geometry, 5186), 4326),
       ST_Transform(ST_SetSRID(emd._geometry, 5186), 4326)
       );
     ```