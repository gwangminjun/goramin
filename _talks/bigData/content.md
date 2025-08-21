---
title: "[빅데이터] 빅데이터 기초"
collection: talks
type: "Talk"
permalink: _talks/bigData/content
date: 2025-08-04
---

# 공부용 토글박스
- 빅데이터 분석기사 준비용 토글박스

# 01 빅데이터 분석기획
### 데이터 따른 분류

<details>
  <summary>가역 데이터</summary>
    <p><strong>데이터가 변하지 않음 → 분석 결과 재현 가능</strong></p>
</details>
<details>
  <summary>불가역 데이터</summary>
    <p><strong>데이터가 변함 → 분석 결과 재현 불가능</strong></p>
    <p><strong>예시: 로그 데이터, 센서 데이터</strong></p>
</details>


### 데이터 베이스 활용

OLTP(Online Transaction Processing) vs OLAP(Online Analytical Processing)
<details>
  <summary>OLTP</summary>
  <p><strong>트랜잭션 중심, 실시간 처리, 데이터베이스 관리 시스템(DBMS) 사용</strong></p>
  <p><strong>데이터 갱신</strong></p>
  <p><strong>예시: 은행 거래, 온라인 쇼핑몰 주문</strong></p> 
</details>
<details>
  <summary>OLAP</summary>
  <p><strong>분석 중심, 실시간 처리 무작위, 데이터베이스 관리 시스템(DBMS) 사용</strong></p>
    <p><strong>데이터 분석 및 조회</strong></p>
    <p><strong>예시: 데이터 웨어하우스, 비즈니스 인텔리전스</strong></p>
</details>

### 빅데이터의 특징

<details>
  <summary>Volume(규모)</summary>
  <p><strong>데이터의 양이 방대함</strong></p>
  <p><strong>예시: 소셜 미디어, IoT 센서 데이터</strong></p>
</details>
<details>
  <summary>Velocity(속도)</summary>
  <p><strong>데이터의 고속성</strong></p>
  <p><strong>예시: 네트워크 통신, IoT 센서 데이터</strong></p>
</details>
<details>
  <summary>Variety(유형)</summary>
  <p><strong>데이터의 다양성</strong></p>
  <p><strong>예시: 소셜 미디어, IoT 센서 데이터</strong></p>
</details>

### 빅데이터의 활용
빅데이터 활용을 위한 3요소
<details>
  <summary>자원</summary>
  <p><strong>다양한 데이터 소스에서 수집된 빅 데이터</strong></p>
  <p><strong>예시: 소셜 미디어, IoT 센서 데이터</strong></p>
</details>
<details>
  <summary>기술</summary>
  <p><strong>빅데이터 처리 및 분석을 위한 기술</strong></p>
  <p><strong>데이터 플랫폼 , AI </strong></p>
  <p><strong>예시: Hadoop, Spark, NoSQL 데이터베이스</strong></p>
</details>
<details>
  <summary>인력</summary>
  <p><strong>빅데이터 분석을 위한 전문 인력</strong></p>
  <p><strong>예시: 데이터 과학자, 데이터 엔지니어</strong></p>
</details>

### 빅데이터 조직 구조
<details>
  <summary>집중형</summary>
    <p><strong>빅데이터 분석팀이 중앙 집중화되어 모든 분석을 수행</strong></p>
    <p><strong>장점: 전문성 집중, 일관된 분석 결과</strong></p>
    <p><strong>단점: 유연성 부족, 부서 간 협업 어려움</strong></p>
</details>
<details>
  <summary>분산형</summary>
    <p><strong>각 부서가 자체적으로 빅데이터 분석을 수행</strong></p>
    <p><strong>장점: 유연성, 부서 간 협업 용이</strong></p>
    <p><strong>단점: 전문성 분산, 일관된 분석 결과 어려움</strong></p>
</details>
<details>
  <summary>혼합형</summary>
    <p><strong>중앙 집중화된 빅데이터 분석팀과 각 부서의 분산형 분석팀이 협력</strong></p>
    <p><strong>장점: 전문성 집중과 유연성의 조화</strong></p>
    <p><strong>단점: 협업 및 조정 필요</strong></p>
</details>

### 지식의 피라미드
<details>
  <summary>데이터</summary>
  <p><strong>원시 데이터, 의미 없는 숫자나 문자</strong></p>
  <p><strong>예시: 센서 데이터, 로그 파일</strong></p>
</details>
<details>
  <summary>정보</summary>
  <p><strong>데이터를 피라미드로 변환한 정보</strong></p>
    <p><strong>예시: 데이터베이스, 스프레드시트</strong></p>
</details>
<details>
  <summary>지식</summary>
  <p><strong>정보를 피라미드로 변환한 지식</strong></p>
  <p><strong>예시: 데이터베이스, 스프레드시트</strong></p>
</details>
<details>
  <summary>지혜</summary>
  <p><strong>지식를 피라미드로 변환한 지혜</strong></p>
  <p><strong>예시: 데이터베이스, 스프레드시트</strong></p>
</details>  
    
### 빅데이터 분석
<details>
  <summary>탐구 요인 분석 EFA</summary>
  <p><strong>탐구 요인 분석은 데이터의 구조와 관계를 이해하기 위한 기법</strong></p>
  <p><strong>예시: 상관 분석, 회귀 분석, 군집 분석</strong></p>
</details>
<details>
  <summary>확인 요인 분석 CFA</summary>
  <p><strong>확인 요인 분석은 데이터의 구조와 관계를 검증하기 위한 기법</strong></p>
  <p><strong>예시: 상관 분석, 회귀 분석, 군집 분석</strong></p>
</details>

### 기계학습의 종류
<details>
  <summary>지도학습</summary>
  <p><strong>레이블이 있는 데이터로 학습 → 예측 모델 생성</strong></p>
  <p><strong>예시: 분류, 회귀</strong></p>
</details>
<details>
    <summary>비지도학습</summary>
    <p><strong>레이블이 없는 데이터로 학습 → 데이터 구조 이해</strong></p>
    <p><strong>예시: 군집화, 차원 축소</strong></p>
</details>
<details>
  <summary>준지도학습</summary>
  <p><strong>레이블이 일부 있는 데이터로 학습 → 예측 모델 생성</strong></p>
  <p><strong>예시: 분류, 회귀</strong></p>
</details>
<details>
  <summary>강화학습</summary>
  <p><strong>환경과 상호작용하며 학습 → 최적의 행동 선택</strong></p>
  <p><strong>예시: 게임, 로봇 제어</strong></p>
</details>

### 개인정보의 이전
<details>
  <summary>개인정보의 처리위탁</summary>
  <p><strong>개인정보를 제3자에게 위탁하여 처리하는 것</strong></p>
  <p><strong>예시: 클라우드 서비스 제공업체에 데이터 저장</strong></p>
</details>
<details>
    <summary>개인정보의 제3자 제공</summary>
    <p><strong>개인정보를 제3자에게 제공하는 것</strong></p>
    <p><strong>예시: 광고 회사에 사용자 데이터 제공</strong></p>
</details>

### 데이터3법
<details>
  <summary>개인정보 보호법</summary>
  <p><strong>개인정보의 수집, 이용, 제공 등에 관한 법률</strong></p>
  <p><strong>목적: 개인정보 보호 및 개인의 권리 보장</strong></p>
</details>
<details>
  <summary>개인정보 제3자 제공법</summary>
    <p><strong>개인정보를 제3자에게 제공하는 경우의 법률</strong></p>
    <p><strong>목적: 개인정보 보호 및 개인의 권리 보장</strong></p>
</details>
<details>
  <summary>정보통신망법</summary>
  <p><strong>정보통신망의 이용 및 정보보호에 관한 법률</strong></p>
  <p><strong>목적: 정보통신망의 안전성 확보 및 개인정보 보호</strong></p>
</details>

### 개인정보 비식별화 조치 가이드라인
<details>
  <summary>가명처리</summary>
  <p><strong>개인정보를 특정할 수 없도록 처리하는 것</strong></p>
  <p><strong>예시: 이름, 주민등록번호 등을 제거</strong></p>
</details>
<details>
    <summary>총계처리</summary>
    <p><strong>개인정보를 집계하여 특정 개인을 식별할 수 없도록 처리하는 것</strong></p>
    <p><strong>예시: 연령대별, 성별 통계</strong></p>
</details>
<details>
  <summary>데이터삭제</summary>
  <p><strong>개인정보를 완전히 삭제하는 것</strong></p>
  <p><strong>예시: 데이터베이스에서 개인정보 레코드 삭제</strong></p>
</details>
<details>
  <summary>데이터 범주화</summary>
  <p><strong>개인정보를 범주로 나누어 특정 개인을 식별할 수 없도록 처리하는 것</strong></p>
  <p><strong>예시: 연령대, 지역 등으로 범주화</strong></p>
</details>
<details>
  <summary>데이터 마스킹</summary>
  <p><strong>개인정보를 특정할 수 없도록 변환하는 것</strong></p>
  <p><strong>예시: 주민등록번호를 XXXX-XXXX로 변환</strong></p>
</details>




### KDD 분석방법론
<details>
  <summary>프로세스 개수</summary>
  <p><strong>9가지</strong></p>
</details>
<details>
  <summary>KDD 분석방법론</summary>
  <p><strong>Knowledge Discovery in Databases</strong></p>
  <p><strong>데이터베이스에서 지식을 발견하는 과정</strong></p>
    <p><strong>단계: 데이터 수집, 전처리, 탐색, 모델링, 결과 해석</strong></p>
</details>
<details>
  <summary>단계</summary>
  <p><strong>1. 데이터 수집</strong></p>
  <p><strong>2. 데이터 전처리</strong></p>
  <p><strong>3. 데이터 탐색</strong></p>
  <p><strong>4. 데이터 모델링</strong></p>
  <p><strong>5. 결과 해석</strong></p>
</details>

### CRISP-DM 분석방법론
<details>
  <summary>프로세스 개수</summary>
  <p><strong>6가지</strong></p>
</details>


<details>
  <summary>4계층</summary>
  <p><strong>최상위 레벨</strong></p>
  <p><strong>일반화 태스크</strong></p>
  <p><strong>세분화 태스크</strong></p>
  <p><strong>프로세스 실행</strong></p>
</details>

### SEMMA 분석방법론
<details>
  <summary>프로세스 개수</summary>
  <p><strong>5가지</strong></p>
</details>


### 빅데이터 분석 방법론 계층
<details>
  <summary>구성</summary>
  <p><strong>단계-태스크-스텝</strong></p>
</details>
<details>
    <summary>단계</summary>
    <p><strong>기준선 설정 , 버전관리를 통한 통제</strong></p>
    <p><strong>예시: 데이터 수집, 전처리, 탐색, 모델링, 결과 해석</strong></p>
</details>
<details>
  <summary>태스크</summary>
  <p><strong>프로세스의 세부 작업</strong></p>
  <p><strong>예시: 데이터 수집, 전처리, 탐색, 모델링, 결과 해석</strong></p>
</details>
<details>
    <summary>스텝</summary>
    <p><strong>태스크의 세부 단계</strong></p>
    <p><strong>예시: 데이터 수집 → 데이터베이스에서 데이터 추출, 전처리 → 결측치 처리, 이상치 제거</strong></p>
</details>

### 데이터 분석 거버넌스 구성요소
<details>
  <summary>구성요소</summary>
  <p><strong>조직</strong></p>
  <p><strong>운영 프로세스</strong></p>
  <p><strong>인프라</strong></p>
  <p><strong>거버넌스</strong></p>
  <p><strong>교육 및 육성체계</strong></p>
</details>

### 데이터 분석 거버넌스 주요 관리 대상
<details>
  <summary>주요 관리 대상</summary>
  <p><strong>마스터 데이터</strong></p>
  <p><strong>메타 데이터</strong></p>
  <p><strong>데이터 사전</strong></p>
</details>

### 데이터 거버넌스의 구성요소
원칙 조직 프로세스
<details>
  <summary>구성요소</summary>
  <p><strong>원칙</strong></p>
  <p><strong>조직</strong></p>
  <p><strong>프로세스</strong></p>
</details>

### 분석 준비도와 분석 성숙도
<details>
  <summary>분석 준비도</summary>
  <p><strong>조직이 분석을 수행할 준비가 되어 있는 정도 6개 영역</strong></p>
  <p><strong>예시: 데이터 수집, 전처리, 탐색, 모델링, 결과 해석</strong></p>
</details>

<details>
  <summary>분석 성숙도</summary>
  <p><strong>조직이 분석을 수행하는 능력의 수준 3개 영역</strong></p>
    <p><strong>비즈니스 , 조직 및 역량 , IT</strong></p>
  <p><strong>예시: 데이터 수집, 전처리, 탐색, 모델링, 결과 해석</strong></p>
</details>

### 분석 성숙도 사분면 분석
<details>
  <summary>사분면 분석</summary>
  <p><strong>조직의 분석 성숙도를 4개의 사분면으로 나누어 분석</strong></p>
</details>

정착형 확산형 준비형 도입형



# 02 빅데이터 탐색

# 03 빅데이터 모델링

# 04 빅데이터 결과 해석


## 결측(MCAR/MAR/MNAR)
<details>
  <summary>MCAR</summary>
  <p><strong>완전무작위 결측(데이터와 무관) → 분석 영향 최소</strong></p>
  <p><strong>그 값 자체가 결측을 좌우하는 경우</strong></p>
</details>
<details>
  <summary>MAR</summary>
  <p><strong>관측값에 의해 설명 가능(미관측값과는 무관) → 적절한 보정 시 불편성 가능</strong></p>
  <p><strong>그 값 자체가 결측을 좌우하는 경우</strong></p>
</details>
<details>
  <summary>MNAR</summary>
  <p><strong>미관측값 자체와 연관 → 모델링/가정 필요, 가장 까다로움</strong></p>
  <p><strong>그 값 자체가 결측을 좌우하는 경우</strong></p>
</details>

## 이상치(IQR, z-점수)  
<details>
  <summary>IQR</summary>
  <p><strong>IQR = Q3 - Q1</strong></p>
  <p><strong>Q1−1.5×IQR 미만, Q3+1.5×IQR 초과면 이상치 후보</strong></p>  
</details>
<details>
  <summary>z-점수</summary>
  <p><strong>z-점수 = (x - μ) / σ</strong></p>
  <p><strong>z-점수 1.96 이상 또는 -1.96 이하면 이상치 후보</strong></p>
</details>

## 스케일링
<details>
  <summary>표준화(Standardization)</summary>
  <p><strong>평균 0, 분산 1로 변환</strong></p>
  <p><strong>표준화 평균 0, 분산 1로 변환</strong></p>
</details>

<details>
  <summary>정규화(Min–Max)</summary>
  <p><strong>0~1 사이로 변환</strong></p>
  <p><strong>정규화 0~1 사이로 변환</strong></p>
  <p><strong>(x−min)/(max−min)</strong></p>
</details>

## 표본분포/신뢰구간 핵심
<details>
  <summary>표본분포</summary>
  <p><strong>𝑋ˉ의 평균=μ, 분산=σ²/n (CLT로 정규 근사)</strong></p>
</details>
<details>
  <summary>평균 신뢰구간</summary>
  <p><strong>𝑋ˉ±1.96×σ/√n</strong></p>
</details>
<details>
  <summary>비율 신뢰구간</summary>
  <p><strong>𝑝ˉ±1.96×√(𝑝ˉ(1−𝑝ˉ)/n)</strong></p>
</details>

## 평균 신뢰구간 선택 규칙
<details>
  <summary>모분산(σ²) ‘앎’ → z</summary>
  <p><strong>𝑋ˉ±1.96×σ/√n</strong></p>
</details>
<details>
  <summary>모분산(σ²) ‘모른다’ → t</summary>
  <p><strong>𝑋ˉ±t(n-1)×s/√n</strong></p>
</details>

## 평균 신뢰구간 자유도
<details>
  <summary>t-분포</summary>
  <p><strong>df=n−1</strong></p>
</details>

<details>
  <summary>z-분포</summary>
  <p><strong>자유도 없음(고정된 표준정규)</strong></p>
</details>
