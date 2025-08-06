---
title: "[리눅스마스터] 공부용 토글박스"
collection: talks
type: "Talk"
permalink: _talks/LinuxMaster/togglebox/content
date: 2025-08-04
---

# 공부용 토글박스

## 개요
  - 원래는.. 노션으로 토글박스 만들어서 하고있었는데
  - 무료 버전에서는 토글박스가 100개로 제한되어 있어서
  - 지웠는데도 계속 100개로 제한되어 있어서
  - 토글박스 기능을 지원하는 다른 곳을 찾아보던 중
  - 이곳을 발견했다 (걍 내가 만듬 ㅋㅋ)

## 각 라이선스 비교
- 오픈소스 라이선스
    <details>
      <summary>수정한 소스는 공개해야 함</summary>
      <p>MPL (Mozilla Public License)</p>
    </details>
    <details>
      <summary>매우 자유로운 라이선스 (Apache와 유사)</summary>
      <p>BSD</p> 
    </details>
    <details>
      <summary>상업적 사용 가능은 하나, 라이브러리 연결 방식에 따라 소스 공개 요구</summary>
      <p>LGPL (Lesser GPL)</p>
    </details>
    <details>
      <summary>공개된 코드로 만든 파생물도 꼭 공개해야 함</summary>
      <p>GPL (GNU General Public License)</p>
    </details>
    <details>
      <summary>상업적 사용 가능, 소스 공개 요구 없음</summary>
      <p>MIT</p>
    </details>

- 카피레프트 기준
    <details>
      <summary>강한 카피레프트</summary>
      <p>GPL</p>
      <p>파생물도 반드시 오픈</p>
    </details>
    <details>
      <summary>약한 카피레프트</summary>
      <p>LGPL, MPL</p>
      <p>수정한 부분만 공개</p>
    </details>
    <details>
      <summary>비카피레프트</summary>
      <p>MIT, BSD, Apache</p>
      <p>수정한 부분 공개 안 해도 됨</p>
    </details>
---
## 리눅스 부팅 전체 흐름 요약
- 리눅스 부팅 과정은 크게 BIOS/UEFI, 부트로더, 커널 로딩, 초기화 프로세스, 사용자 공간으로 나뉩니다.
    <details>
      <summary>리눅스 부팅 전체 흐름 요약</summary>
      <p>리눅스 부팅 과정은 크게 BIOS/UEFI, 부트로더, 커널 로딩, 초기화 프로세스, 사용자 공간으로 나뉩니다.</p>
      <ul>
        <li><strong>BIOS/UEFI:</strong> 하드웨어 초기화 및 부트 디바이스 선택</li>
        <li><strong>부트로더:</strong> 커널 이미지와 초기 램 디스크를 메모리에 로드</li>
        <li><strong>커널 로딩:</strong> 커널이 하드웨어를 인식하고 초기화</li>
        <li><strong>초기화 프로세스:</strong> init 프로세스가 시작되어 시스템 서비스와 데몬을 실행</li>
        <li><strong>사용자 공간:</strong> 로그인 프롬프트 또는 GUI 환경 제공</li>
      </ul>
        <p>이 과정은 시스템의 하드웨어와 소프트웨어가 상호작용하여 최종적으로 사용자에게 인터페이스를 제공하는 것을 목표로 합니다.</p>
    </details>
    <details>
      <summary>운영체제 선택, 커널(vmlinuz) + initrd 로드</summary>
      <p>부트로더 (GRUB)</p>
    </details>
    <details>
      <summary>PID 1번 프로세스 실행</summary>
      <p>init (또는 systemd)</p>
    </details>
    <details>
      <summary>하드웨어 초기화 및 루트 파일시스템 마운트</summary>
      <p>커널 (vmlinuz)</p>
    </details>
---
## RUNLevels
- RUNLevel은 리눅스 시스템의 실행 상태를 정의하는 개념입니다.
    <details>
      <summary>RUNLevel 0</summary>
      <p>시스템 종료</p>
    </details>
    <details>
      <summary>RUNLevel 1</summary>
      <p>단일 사용자 모드 (시스템 유지보수)</p>
    </details>
    <details>
      <summary>RUNLevel 2</summary>
      <p>멀티 사용자 모드 (네트워크 서비스 없음)</p>
    </details>
    <details>
      <summary>RUNLevel 3</summary>
      <p>멀티 사용자 모드 (네트워크 서비스 포함)</p>
    </details>
    <details>
      <summary>RUNLevel 4</summary>
      <p>사용자 정의 모드 (일반적으로 사용되지 않음)</p>
    </details>
    <details>
      <summary>RUNLevel 5</summary>
      <p>멀티 사용자 모드 (GUI 포함)</p>
    </details>
    <details>
      <summary>RUNLevel 6</summary>
      <p>시스템 재부팅</p>
    </details>  
---
## systemd Target
- systemd는 RUNLevel을 대체하는 타겟(target) 개념을 사용합니다.
    <details>
      <summary>target: graphical.target</summary>
      <p>GUI 환경을 제공하는 타겟</p>
    </details>
    <details>
      <summary>target: multi-user.target</summary>
      <p>멀티 사용자 모드 (네트워크 서비스 포함) 	CLI 환경 (네트워크 포함) </p>
    </details>
    <details>
      <summary>target: rescue.target</summary>
      <p>단일 사용자 모드 (시스템 유지보수)</p>
    </details>
    <details>
      <summary>target: emergency.target</summary>
      <p>긴급 모드 (최소한의 서비스만 실행)</p>
    </details>
    <details>
      <summary>target: reboot.target</summary>
      <p>시스템 재부팅을 위한 타겟</p>
    </details>
    <details>
      <summary>target: poweroff.target</summary>
      <p>시스템 종료를 위한 타겟</p>
    </details>
    <details>
      <summary>target: default.target</summary>
      <p>기본 타겟 (일반적으로 graphical.target 또는 multi-user.target)</p>
    </details>
---
- 관련 명령어
    <details>
        <summary>systemctl get-default</summary>
        <p>현재 시스템의 기본 타겟을 확인합니다.</p>
    </details>
    <details>
        <summary>sudo systemctl set-default multi-user.target</summary>
        <p>시스템의 기본 타겟을 설정합니다.</p>
    </details>
    <details>
        <summary>sudo systemctl isolate graphical.target</summary>
        <p>즉시 해당 타겟으로 전환</p>
    </details>
---
## 리눅스 사용자 및 계정 관리
- 사용자 관련 주요 파일
    <details>
        <summary>/etc/passwd</summary>
        <p>사용자 정보</p>
    </details>
    <details>
        <summary>/etc/shadow</summary>
        <p>암호 정보 (암호화된 형태)</p>
    </details>
---
- /etc/passwd 파일 구조
    <details>
        <summary>파일 구조</summary>
        <p>계정명:패스워드:UID:GID:설명:홈디렉토리:쉘</p>
    </details>

---
## 그룹 관련 명령어
- 그룹 관련 주요 파일
    <details>
        <summary>usermod -aG [그룹명] [사용자]</summary>
        <p>사용자를 보조 그룹에 추가</p>
    </details>
    <details>
          <summary>gpasswd</summary>
          <p>그룹 비밀번호 설정</p>
    </details>
---
## RAID
- RAID는 여러 디스크를 하나의 논리적 디스크로 묶어 데이터 보호 및 성능 향상을 도모하는 기술입니다.
    <details>
        <summary>RAID 0</summary>
        <p>스트라이핑 (성능 향상, 데이터 보호 없음)</p>
        <p>최소 2개 디스크</p>
        <p>안전성 없음</p>
    </details>
    <details>
        <summary>RAID 1</summary>
        <p>미러링 (데이터 보호, 성능 향상)</p>
        <p>최소 2개 디스크</p>
        <p>안전성 최고</p>
    </details>
    <details>
        <summary>RAID 5</summary>
        <p>패리티 분산 (데이터 보호, 성능 향상) , 스트라이핑 + 패러티</p>
        <p>최소 3개 디스크</p>
        <p>2개 디스크 고장 시 복구 불가</p>
    </details>
    <details>
        <summary>RAID 6</summary>
        <p>RAID 5 + 이중 패리티 (더 높은 데이터 보호)</p>
        <p>최소 4개 디스크</p>
        <p>2개 고장 복구</p>
    </details>
    <details>
        <summary>RAID 10</summary>
        <p>RAID 1과 RAID 0의 조합 (고성능 및 데이터 보호)</p>
        <p>최소 4개 디스크</p>
        <p>속도+안정성 모두 OK</p>
    </details>
  
---

## LVM (Logical Volume Manager)





