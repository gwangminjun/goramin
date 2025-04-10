---
title: "git 저장소 용량 문제 해결"
collection: teaching
type: "webEvent"
permalink: /teaching/largeGitRepository/content
venue: "직장"
date: 2025-04-10
---
# git 저장소 용량 문제 해결

## 상황
```shell
4.0K    HEAD
4.0K    branches
4.0K    config
4.0K    description
52K     hooks
8.0K    info
1.3G    objects
16K     refs
```
- git 저장소의 용량이 1.3G로 너무 커서 git clone이 불가함

## 해결
1. 얕은 클론(Shallow Clone) 사용하기
    ```bash
      git clone --depth 1 <repository-url>
    ```
   이 방법은 최신 커밋만 가져오므로 전체 히스토리를 다운로드하지 않아 용량이 크게 줄어듭니다.
2. 특정 브랜치만 클론하기
    ```bash
        git clone --single-branch --branch <branch-name> <repository-url>
    ```
    이 방법은 특정 브랜치만 클론하여 다른 브랜치의 데이터를 받지 않습니다.
3. 위 두 방법 결합하기
    ```bash
        git clone --depth 1 --single-branch --branch <branch-name> <repository-url>
    ```
## git clone 후 저장소 정리
   - git clone 후 저장소의 용량을 줄이기 위해서는 다음과 같은 방법을 사용할 수 있습니다.
    ```bash
    git gc --prune=now
    ```
    - `git gc` 명령어는 저장소의 가비지 컬렉션을 수행하여 불필요한 파일을 정리합니다.
   - `--prune=now` 옵션은 즉시 가비지 컬렉션을 수행하여 더 이상 사용되지 않는 객체를 삭제합니다.
    - 이 명령어를 사용하면 저장소의 용량을 줄일 수 있습니다.
