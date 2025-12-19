# goramin 블로그 작성 가이드

이 문서는 goramin 블로그에 새로운 콘텐츠를 작성하는 방법을 설명합니다.

## 목차

1. [빠른 시작](#빠른-시작)
2. [콘텐츠 타입별 작성법](#콘텐츠-타입별-작성법)
3. [마크다운 작성법](#마크다운-작성법)
4. [이미지 추가하기](#이미지-추가하기)
5. [로컬에서 미리보기](#로컬에서-미리보기)
6. [배포하기](#배포하기)

---

## 빠른 시작

### 1. 작성할 콘텐츠 타입 선택

블로그에는 4가지 주요 콘텐츠 타입이 있습니다:

- **Teaching**: 기술 튜토리얼, 문제 해결 방법 등
- **Publications**: 심화 학습 내용, 기술 문서
- **Posts**: 일반 블로그 포스트
- **Portfolio**: 프로젝트 소개 및 경력

### 2. 해당 폴더에 파일 생성

각 타입에 맞는 폴더에 마크다운 파일을 생성합니다:

```
_teaching/      → Teaching 문서
_publications/  → Publications 문서
_posts/         → Blog Posts
_portfolio/     → Portfolio 항목
```

### 3. Front Matter 작성

파일 맨 위에 YAML 형식의 메타데이터를 작성합니다 (자세한 내용은 아래 참조).

### 4. 본문 작성

Front Matter 아래에 마크다운 형식으로 본문을 작성합니다.

---

## 콘텐츠 타입별 작성법

### Teaching 문서 작성하기

**파일 위치**: `_teaching/폴더명/content.md` 또는 `_teaching/파일명.md`

**Front Matter 형식**:
```yaml
---
title: "문서 제목"
collection: teaching
type: "카테고리명"
permalink: /teaching/폴더명/content
venue: "작성 장소"
date: YYYY-MM-DD
---
```

**예시**:
```markdown
---
title: "Debounce 와 throttle 에 대해서"
collection: teaching
type: "webEvent"
permalink: /teaching/debounceThrottle/content
venue: "직장"
date: 2024-06-27
---

## Debounce

함수를 마지막으로 호출한 후 일정 시간이 경과한 후에만 함수가 실행됩니다.

### 사용 예시
- 검색창 자동완성
- 윈도우 리사이징 이벤트

## 참조
- https://example.com
```

**폴더 구조 추천**:
```
_teaching/
  └── debounceThrottle/
      ├── content.md
      ├── img.png
      └── img_1.png
```

---

### Publications 문서 작성하기

**파일 위치**: `_publications/YYYY-MM-DD-제목.md`

**Front Matter 형식**:
```yaml
---
title: "출판물 제목"
collection: publications
permalink: /publication/YYYY-MM-DD-제목
excerpt: '간단한 설명'
date: YYYY-MM-DD
venue: 'Journal 번호'
citation: '인용 정보 (선택사항)'
---
```

**예시**:
```markdown
---
title: "JPA에 대해 알아보자"
collection: publications
permalink: /publication/2024-06-14-JPA
excerpt: 'JPA 에 대해서 알아보자'
date: 2024-06-14
venue: 'Journal 3'
citation: 'min jun Yang. (2024). &quot; JPA &quot; <i>Journal 3</i>. 1(1).'
---

# JPA란?

Java Persistence API의 약자로...

## JPA의 장점
1. 객체 지향적인 코드
2. 생산성 향상
3. 유지보수 용이

## 참조
- https://example.com
```

---

### Blog Posts 작성하기

**파일 위치**: `_posts/YYYY-MM-DD-제목.md` 또는 `_posts/폴더명/content.md`

**Front Matter 형식**:
```yaml
---
title: '포스트 제목'
date: YYYY-MM-DD
permalink: /posts/제목/
tags:
  - tag1
  - tag2
  - tag3
---
```

**예시**:
```markdown
---
title: 'AST 에 대하여'
date: 2024-06-12
permalink: /posts/AST/content
tags:
  - javascript
  - compiler
  - Transpiler
  - Tech
---

### 서문
주말마다 하는 모던 자바스크립트 책 스터디가 있는데...

### 본문
AST(Abstract Syntax Tree)는...

### 참조
- https://example.com
```

---

### Portfolio 작성하기

**파일 위치**: `_portfolio/파일명.md`

**Front Matter 형식**:
```yaml
---
title: "포트폴리오 제목"
excerpt: "간단한 설명"
collection: portfolio
---
```

**예시**:
```markdown
---
title: "웹 개발 포트폴리오"
excerpt: "웹 개발 경력 및 프로젝트 소개"
collection: portfolio
---

## 소개
안녕하세요! 저는 웹 개발자입니다.

## 기술 스택
- Front-end: JavaScript, jQuery
- Back-end: Spring, MyBatis

## 프로젝트 경험
### 1. 프로젝트명
- 기간: 2024.01 - 2024.06
- 설명: 프로젝트 설명
```

---

## 마크다운 작성법

### 기본 문법

#### 제목
```markdown
# 제목 1
## 제목 2
### 제목 3
#### 제목 4
```

#### 텍스트 강조
```markdown
**굵게**
*기울임*
~~취소선~~
`코드`
```

#### 목록
```markdown
# 순서 없는 목록
- 항목 1
- 항목 2
  - 하위 항목

# 순서 있는 목록
1. 첫 번째
2. 두 번째
3. 세 번째
```

#### 링크
```markdown
[링크 텍스트](https://example.com)
[이메일](mailto:gnb1215@naver.com)
```

#### 코드 블록
````markdown
```java
public class Example {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

```javascript
const greeting = "Hello World";
console.log(greeting);
```
````

#### 인용문
```markdown
> 이것은 인용문입니다.
> 여러 줄로 작성할 수 있습니다.
```

#### 표
```markdown
| 항목 | 설명 | 비고 |
|------|------|------|
| A | 설명A | 비고A |
| B | 설명B | 비고B |
```

#### 줄바꿈
```markdown
# 방법 1: <br> 태그 사용
첫 번째 줄<br>
두 번째 줄

# 방법 2: 공백 두 개 + 엔터
첫 번째 줄
두 번째 줄
```

---

## 이미지 추가하기

### 방법 1: 콘텐츠 폴더 내 이미지 (추천)

**Teaching/Posts의 경우**:
```
_teaching/
  └── myTopic/
      ├── content.md
      ├── img.png
      ├── img_1.png
      └── img_2.png
```

**마크다운에서 사용**:
```markdown
![이미지 설명](img.png)
![다른 이미지](img_1.png)
```

### 방법 2: images 폴더 사용

1. 이미지를 `images/` 폴더에 저장
2. 마크다운에서 참조:
```markdown
![이미지 설명](/images/myimage.png)
```

### 방법 3: 외부 URL 사용

```markdown
![이미지 설명](https://example.com/image.png)
```

### 이미지 크기 조절 (HTML 사용)

```html
<img src="img.png" alt="이미지 설명" width="500">
<img src="img.png" alt="이미지 설명" style="width: 50%;">
```

---

## 로컬에서 미리보기

작성한 글을 배포하기 전에 로컬에서 미리 확인할 수 있습니다.

### 1. Jekyll 서버 실행

```bash
# 저장소 루트 디렉토리에서
jekyll serve -l -H localhost

# 또는
bundle exec jekyll serve -l -H localhost
```

### 2. 브라우저에서 확인

브라우저를 열고 다음 주소로 이동:
```
http://localhost:4000
```

### 3. 실시간 수정 확인

- Jekyll 서버가 실행 중일 때 파일을 수정하면 자동으로 재빌드됩니다
- 브라우저를 새로고침하면 변경사항을 확인할 수 있습니다
- `_config.yml` 파일을 수정한 경우에는 서버를 재시작해야 합니다

### 문제 해결

**포트가 이미 사용 중인 경우**:
```bash
jekyll serve -l -H localhost --port 4001
```

**캐시 문제 해결**:
```bash
bundle exec jekyll clean
bundle exec jekyll serve -l -H localhost
```

---

## 배포하기

### GitHub Pages로 자동 배포

이 블로그는 GitHub Pages를 사용하여 자동으로 배포됩니다.

#### 1. 변경사항 커밋

```bash
# 변경된 파일 확인
git status

# 파일 추가
git add .

# 커밋
git commit -m "새 글 작성: [글 제목]"
```

#### 2. GitHub에 푸시

```bash
git push origin master
```

#### 3. 배포 확인

- GitHub Actions가 자동으로 빌드 및 배포를 진행합니다
- 몇 분 후 https://gwangminjun.github.io/goramin 에서 확인할 수 있습니다
- GitHub 저장소의 "Actions" 탭에서 배포 상태를 확인할 수 있습니다

### 배포 전 체크리스트

- [ ] 로컬에서 미리보기로 확인했는가?
- [ ] Front Matter가 올바르게 작성되었는가?
- [ ] 모든 이미지가 정상적으로 표시되는가?
- [ ] 링크가 올바르게 동작하는가?
- [ ] 오타나 문법 오류가 없는가?
- [ ] 코드 블록의 언어가 지정되어 있는가?

---

## 팁 & 트릭

### 1. 파일명 규칙

- **Posts**: `YYYY-MM-DD-제목.md` 형식 사용
- **Publications**: `YYYY-MM-DD-제목.md` 형식 사용
- **Teaching**: 폴더 생성 후 `content.md` 사용 권장 (이미지 관리가 쉬움)

### 2. 이미지 이름 규칙

- 의미 있는 이름 사용: `database-structure.png`
- 또는 번호 사용: `img.png`, `img_1.png`, `img_2.png`

### 3. 날짜 형식

- 항상 `YYYY-MM-DD` 형식 사용
- 예: `2024-06-27`

### 4. 카테고리 및 태그

**Teaching의 type**:
- `webEvent`: 웹 이벤트 관련
- `infra`: 인프라 관련
- 필요에 따라 새로운 타입 추가 가능

**Posts의 tags**:
- 소문자 사용 권장
- 여러 태그 사용 가능
- 예: `javascript`, `java`, `spring`, `database`

### 5. Permalink 규칙

- Teaching: `/teaching/폴더명/content`
- Publications: `/publication/YYYY-MM-DD-제목`
- Posts: `/posts/제목/` 또는 `/posts/폴더명/content`

### 6. 코드 하이라이팅 언어

자주 사용하는 언어 코드:
```
java, javascript, python, bash, sql, yaml, json, html, css, xml
```

### 7. 참조 링크 작성

글 마지막에 참조한 링크를 정리하는 것을 권장합니다:

```markdown
## 참조
- [제목1](https://example.com)
- [제목2](https://example.com)
```

---

## 문제 해결

### Jekyll 서버가 시작되지 않을 때

```bash
# Gemfile.lock 삭제 후 재설치
rm Gemfile.lock
bundle install
```

### 이미지가 표시되지 않을 때

1. 파일 경로 확인
2. 이미지 파일명의 대소문자 확인 (Linux는 대소문자 구분)
3. 이미지 파일이 실제로 존재하는지 확인

### 글이 블로그에 표시되지 않을 때

1. Front Matter 형식이 올바른지 확인
2. 파일명 형식이 올바른지 확인
3. 날짜가 미래 날짜가 아닌지 확인
4. `_config.yml`의 `future: true` 설정 확인

---

## 추가 리소스

- [Jekyll 공식 문서](https://jekyllrb.com/docs/)
- [Markdown 가이드](https://www.markdownguide.org/)
- [Academic Pages 템플릿](https://github.com/academicpages/academicpages.github.io)

---

## 문의

궁금한 점이나 문제가 있으면 언제든지 연락주세요:

- **이메일**: gnb1215@naver.com
- **GitHub Issues**: https://github.com/gwangminjun/goramin/issues

---

행복한 블로깅 되세요! 🎄
