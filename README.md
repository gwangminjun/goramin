# goramin 블로그

![pages-build-deployment](https://github.com/gwangminjun/goramin/actions/workflows/pages/pages-build-deployment/badge.svg)

Jekyll 기반의 개인 기술 블로그입니다. 웹 개발과 관련된 다양한 기술 문서와 학습 내용을 공유합니다.

## 블로그 소개

**goramin 블로그**는 웹 개발자 Yang Min Jun의 기술 블로그입니다.
실무에서 경험한 내용과 학습한 기술들을 정리하여 공유하고 있습니다.

- **블로그 주소**: https://gwangminjun.github.io/goramin
- **작성자**: Yang Min Jun (광주 소재 웹 개발자)
- **GitHub**: [@gwangminjun](https://github.com/gwangminjun)

## 주요 콘텐츠

### 📚 Teaching
웹 개발 실무에서 활용되는 다양한 기술과 개념을 정리한 문서들입니다.

- **JavaScript**: Debounce & Throttle, Promise.allSettled 등
- **Java/Spring**: MyBatis, JPA, Generics 등
- **JSP**: Page Directive, Encoding, Backtick 사용법 등
- **Database**: MySQL, PostgreSQL, PostGIS 등
- **기타**: Git 대용량 저장소 관리, 프로젝트 사례 등

### 📝 Publications
기술 주제별 심화 학습 내용을 정리한 문서들입니다.

- Git 사용법
- Java Collection
- JPA (Java Persistence API)
- Session, Token, Cookie 인증 방식

### 💼 Portfolio
진행한 프로젝트와 작업물을 소개합니다.

### 🎤 Talks
발표 자료와 세미나 내용을 공유합니다.

## 기술 스택

이 블로그는 다음 기술들을 사용하여 구축되었습니다:

- **Jekyll**: 정적 사이트 생성기
- **GitHub Pages**: 호스팅
- **Academic Pages 템플릿**: 학술 웹사이트 테마 기반
- **Ruby & Bundler**: 의존성 관리

## 로컬 환경에서 실행하기

블로그를 로컬 환경에서 실행하고 미리보려면 다음 단계를 따르세요:

### 사전 요구사항

1. Ruby, Ruby-dev, Bundler, Node.js 설치
   ```bash
   # Ubuntu/Debian
   sudo apt install ruby-dev ruby-bundler nodejs

   # Windows
   # Ruby Installer를 사용하여 Ruby 설치
   # https://rubyinstaller.org/
   ```

2. Linux에서 추가 의존성 설치
   ```bash
   sudo apt install build-essential gcc make
   ```

### 실행 방법

1. 저장소 클론
   ```bash
   git clone https://github.com/gwangminjun/goramin.git
   cd goramin
   ```

2. Ruby 의존성 설치
   ```bash
   bundle install
   ```

   오류가 발생하면 `Gemfile.lock`을 삭제하고 다시 시도하세요.

3. Jekyll 서버 실행
   ```bash
   jekyll serve -l -H localhost
   ```

   또는 Bundle을 통해 실행:
   ```bash
   bundle exec jekyll serve -l -H localhost
   ```

4. 브라우저에서 `http://localhost:4000` 접속

로컬 서버는 파일 변경사항을 자동으로 감지하고 페이지를 다시 빌드합니다.

## 프로젝트 구조

```
goramin/
├── _config.yml           # Jekyll 설정 파일
├── _data/                # 데이터 파일 (authors, navigation 등)
├── _includes/            # 재사용 가능한 HTML 조각
├── _layouts/             # 페이지 레이아웃 템플릿
├── _pages/               # 정적 페이지
├── _posts/               # 블로그 포스트
├── _teaching/            # 기술 문서 콘텐츠
├── _publications/        # 학습 문서 콘텐츠
├── _portfolio/           # 포트폴리오 항목
├── _talks/               # 발표 자료
├── assets/               # CSS, JavaScript, 이미지 등
├── files/                # 다운로드 가능한 파일
└── images/               # 블로그 이미지
```

## 콘텐츠 추가하기

### 새 Teaching 문서 추가

`_teaching/` 폴더에 새 마크다운 파일을 생성합니다:

```markdown
---
title: "문서 제목"
collection: teaching
type: "카테고리"
permalink: /teaching/문서경로/
venue: "장소"
date: YYYY-MM-DD
---

여기에 내용을 작성합니다.
```

### 새 Publication 추가

`_publications/` 폴더에 새 마크다운 파일을 생성합니다:

```markdown
---
title: "출판물 제목"
collection: publications
permalink: /publication/YYYY-MM-DD-제목
excerpt: '간단한 설명'
date: YYYY-MM-DD
---

여기에 내용을 작성합니다.
```

## 설정 변경하기

블로그의 주요 설정은 `_config.yml` 파일에서 변경할 수 있습니다:

- 사이트 제목, 설명
- 작성자 정보
- 소셜 미디어 링크
- Google Analytics 설정
- 테마 및 레이아웃 설정

설정 파일을 수정한 후에는 Jekyll 서버를 재시작해야 합니다.

## 기여하기

버그 리포트나 기능 제안은 [GitHub Issues](https://github.com/gwangminjun/goramin/issues)를 통해 제출해 주세요.

## 라이선스

이 프로젝트는 [Academic Pages](https://github.com/academicpages/academicpages.github.io) 템플릿을 기반으로 하며,
원본 템플릿은 [Minimal Mistakes Jekyll Theme](https://mmistakes.github.io/minimal-mistakes/)에서 포크되었습니다.

원본 테마는 © 2016 Michael Rose이며 MIT 라이선스 하에 배포됩니다. (LICENSE.md 참조)

## 문의

- **이메일**: gnb1215@naver.com
- **GitHub**: [@gwangminjun](https://github.com/gwangminjun)

---

방문해 주셔서 감사합니다! 오늘도 행복한 하루 되세요! 🎄
