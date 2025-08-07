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

- 구성요소
    <details>
        <summary>Physical Volume (PV)</summary>
        <p>물리적 디스크 또는 파티션</p>
    </details>
    <details>
        <summary>Physical Extent (PE)</summary>
        <p>PV의 부분 물리적 디스크</p>
    </details>
    <details>
        <summary>Volume Group (VG)</summary>
        <p>여러 PV를 묶은 논리적 그룹</p>
    </details>
    <details>
        <summary>Logical Volume (LV)</summary>
        <p>VG에서 할당된 논리적 디스크</p>
    </details>
    
---

## 부트 매니저
- 부트 매니저는 시스템 부팅 시 운영체제를 선택하고 로드하는 역할을 합니다.
- 순서 : BIOS/UEFI → 부트 매니저 → 커널 로딩
    <details>
        <summary>GRUB (GRand Unified Bootloader)</summary>
        <p>가장 널리 사용되는 부트로더로, 다양한 운영체제를 지원합니다.</p>
    </details>
    <details>
        <summary>LILO (Linux Loader)</summary>
        <p>과거에 사용되던 부트로더로, 현재는 GRUB이 대체하고 있습니다.</p>
    </details>
    <details>
        <summary>systemd-boot</summary>
        <p>systemd 기반의 부트로더로, UEFI 시스템에서 사용됩니다.</p>
    </details>


- GRUB (GRand Unified Bootloader) 구성파일
    <details>
        <summary>/etc/default/grub</summary>
        <p>GRUB 설정 파일로, 부트 메뉴 옵션 등을 정의합니다.</p>
        <p>사용자가 설정 수정하는 파일</p>
    </details>
    <details>
        <summary>/boot/grub/grub.cfg</summary>
        <p>GRUB의 실제 구성 파일로, 부트 메뉴 항목을 포함합니다.</p>
    </details>
    <details>
        <summary>/etc/grub.d/</summary>
        <p>grub.cfg를 만드는 스크립트들이 있는 디렉터리</p>
    </details>

## 리눅스 주요 디렉터리
- 리눅스 주요 디렉터리
    <details>
        <summary>/etc</summary>
        <p>시스템 설정 파일이 위치하는 디렉터리</p>
    </details>
    <details>
        <summary>/var</summary>
        <p>가변 데이터 파일이 위치하는 디렉터리 (로그, 캐시 등)</p>
    </details>
    <details>
        <summary>/usr</summary>
        <p>사용자 프로그램과 라이브러리가 위치하는 디렉터리</p>
    </details>
    <details>
        <summary>/bin</summary>
        <p>시스템 필수 실행 파일이 위치하는 디렉터리</p>
    </details>
    <details>
        <summary>/sbin</summary>
        <p>시스템 관리용 실행 파일이 위치하는 디렉터리</p>
    </details>
    <details>
        <summary>/lib</summary>
        <p>시스템 라이브러리가 위치하는 디렉터리</p>
    </details>
    <details>
        <summary>/home</summary>
        <p>사용자 홈 디렉터리가 위치하는 디렉터리</p>
    </details>  
    <details>
        <summary>/dev</summary>
        <p>디바이스 파일이 위치하는 디렉터리</p>
    </details>
    <details>
        <summary>/proc</summary>
        <p>프로세스 정보와 시스템 정보를 제공하는 가상 파일 시스템</p>
    </details>
    <details>
        <summary>/sys</summary>
        <p>커널과 시스템 정보를 제공하는 가상 파일 시스템</p>
    </details>
    <details>
        <summary>/tmp</summary>
        <p>임시 파일이 위치하는 디렉터리</p>
    </details>
    <details>
        <summary>/boot</summary>
        <p>부팅 관련 파일이 위치하는 디렉터리 (커널 이미지 등)</p>
    </details>
    <details>
        <summary>/mnt</summary>
        <p>임시 마운트 지점으로 사용되는 디렉터리</p>
    </details>
    <details>
        <summary>/opt</summary>
        <p>추가 소프트웨어 패키지가 위치하는 디렉터리</p>
    </details>

---
## 파일시스템
- 파일시스템은 디렉터리와 파일의 맵을 만드는 시스템이다.
- 리눅스에서 사용되는 주요 파일시스템
    <details>
        <summary>ext4</summary>
        <p>리눅스에서 가장 널리 사용되는 파일시스템</p>
    </details>
    <details>
        <summary>XFS</summary>
        <p>고성능 파일시스템으로 대용량 데이터 처리에 적합</p>
        <p>RedHat 계열에서 기본 사용</p>
    </details>
    <details>
        <summary>Btrfs</summary>
        <p>스냅샷, RAID 기능 등을 지원하는 최신 파일시스템</p>
    </details>
    <details>
        <summary>FAT32</summary>
        <p>호환성이 높은 파일시스템으로 USB 드라이브 등에 사용</p>
    </details>
    <details>
        <summary>NTFS</summary>
        <p>Windows에서 주로 사용되는 파일시스템, 리눅스에서도 읽기/쓰기 가능</p>
    </details>
    <details>
      <summary>저널링 파일 시스템</summary>
      <p>저널링 파일 시스템은 데이터 무결성을 보장하기 위해 변경 사항을 기록하는 기능을 갖춘 파일 시스템입니다.</p>
    </details>

---
## 블록그룹
- 블록 그룹은 ext4 파일 시스템에서 데이터를 효율적으로 저장하고 관리하기 위한 구조입니다.
    <details>
        <summary>블록 그룹 구조</summary>
        <p>블록 그룹은 파일 시스템을 여러 개의 블록 그룹으로 나누어 각 그룹이 독립적으로 관리됩니다.</p>
        <p>각 블록 그룹은 다음과 같은 요소로 구성됩니다:</p>
        <ul>
            <li>슈퍼블록 (Superblock)</li>
            <li>비트맵 (Bitmap)</li>
            <li>데이터 블록 (Data Blocks)</li>
            <li>인덱스 노드 (Inode Table)</li>
        </ul>
    </details>

- 구성요소
    <details>
        <summary>슈퍼블록(Superblock) 복사본</summary>
        <p>파일 시스템의 메타데이터를 포함하며, 파일 시스템의 크기, 블록 크기, 블록 그룹 수 등을 정의합니다.</p>
    </details>
    <details>
        <summary>그룹 디스크립터</summary>
        <p>파일 시스템의 관리를 위한 그룹 디스크립터</p>
    </details>
    <details>
        <summary>비트맵(블록/아이노드) (Data Blocks)</summary>
        <p>사용 가능한 블록/아이노드 추적</p>
    </details>
    <details>
        <summary>아이노드 테이블 (inode table)</summary>
        <p>파일 메타데이터 저장</p>
    </details>
    <details>
        <summary>데이터 블록</summary>
        <p>실제 파일 데이터 저장 영역</p>
    </details>

---
## X 윈도우
- X 윈도우 시스템은 리눅스에서 그래픽 사용자 인터페이스(GUI)를 제공하는 시스템입니다.

- 구성요소
    <details>
        <summary>X 서버</summary>
        <p>그래픽 하드웨어와 상호작용하여 화면에 그래픽을 출력합니다.</p>
        <p>키보드, 마우스, 모니터 등 장치 제어 + 화면 출력</p>
    </details>
    <details>
        <summary>X 클라이언트</summary>
        <p>사용자 애플리케이션으로, X 서버에 그래픽 요청을 보냅니다.</p>
        <p>	GUI 애플리케이션 (예: 터미널, 브라우저 등)</p>
    </details>
    <details>
        <summary>X 윈도우 매니저</summary>
        <p>윈도우의 모양과 동작을 관리하는 소프트웨어입니다.</p>
        <p>창의 위치, 제목 표시줄 등 창 관리</p>
    </details>

- 환경 차이

| 용어                    | 역할                                           | 예시                 |
| --------------------- | -------------------------------------------- | ------------------ |
| **🖥️ 데스크탑 환경 (DE)**  | 로그인 후 사용하는 **전체 GUI 환경** (바탕화면, 파일 관리자, 창 등) | GNOME, KDE, XFCE   |
| **🔐 디스플레이 매니저 (DM)** | **로그인 화면(GUI)** 을 띄우고 데스크탑 환경을 불러오는 역할       | GDM, LightDM, SDDM |


- 데스크탑 환경
    <details>
        <summary>GNOME</summary>
        <p>사용자 친화적인 인터페이스를 제공하는 데스크탑 환경입니다.</p>
    </details>
    <details>
        <summary>KDE Plasma</summary>
        <p>고급 사용자 정의 기능을 제공하는 데스크탑 환경입니다.</p>
    </details>
    <details>
        <summary>Xfce</summary>
        <p>경량화된 데스크탑 환경으로, 저사양 시스템에서도 원활하게 동작합니다.</p>
    </details>

- 디스플레이 매니저
    <details>
        <summary>GDM (GNOME Display Manager)</summary>
        <p>GNOME / 사용자 로그인 및 세션 관리를 담당하는 소프트웨어입니다.</p>
    </details>
    <details>
        <summary>LightDM</summary>
        <p>XFCE / 경량화된 디스플레이 매니저로, 다양한 데스크탑 환경을 지원합니다.</p>
    </details>
    <details>
        <summary>SDDM (Simple Desktop Display Manager)</summary>
        <p>KDE Plasma와 함께 사용되는 디스플레이 매니저입니다.</p>
    </details>

---
## 셸
- 셸은 사용자와 운영체제 간의 인터페이스 역할을 합니다.
- 셸의 종류
    <details>
        <summary>Bash (Bourne Again SHell)</summary>
        <p>리눅스에서 가장 널리 사용되는 셸로, 스크립트 작성과 명령어 실행에 사용됩니다.</p>
    </details>
    <details>
        <summary>Zsh (Z Shell)</summary>
        <p>강력한 기능과 사용자 정의 옵션을 제공하는 셸입니다.</p>
    </details>
    <details>
        <summary>Fish (Friendly Interactive SHell)</summary>
        <p>사용자 친화적인 인터페이스와 자동 완성 기능을 갖춘 셸입니다.</p>
    </details>

- 셸 환경 설정 파일
    <details>
        <summary>/etc/profile</summary>
        <p>시스템 전체의 셸 환경 설정 파일로, 모든 사용자에게 적용됩니다.</p>
    </details>
    <details>
        <summary>/etc/bash.bashrc</summary>
        <p>Bash 셸의 시스템 전체 환경 설정 파일로, 모든 사용자에게 적용됩니다.</p>
    </details>
    <details>
        <summary>~/.bash_profile</summary>
        <p>사용자 개인의 Bash 셸 환경 설정 파일로, 로그인 시 실행됩니다.</p>
    </details>
    <details>
        <summary>~/.bashrc</summary>
        <p>사용자 개인의 Bash 셸 환경 설정 파일로, 인터랙티브 셸에서 실행됩니다.</p>
    </details>
    
- 셸 명령어 정리
    <details>
        <summary>echo</summary>
        <p>문자열 출력</p>
    </details>
    <details>
        <summary>alias</summary>
        <p>명령어에 별칭 설정</p>
    </details>
    <details>
        <summary>source</summary>
        <p>셸 스크립트 또는 설정 파일 재실행</p>
    </details>
    <details>
        <summary>export</summary>
        <p>환경 변수 설정</p>
    </details>
    <details>
        <summary>which </summary>
        <p>명령어의 실행 파일 위치 확인</p>
    </details>
  
## 셸 프로그래밍
- 셸 스크립트는 셸 명령어를 모아 작성한 프로그램입니다.
- 셸 종류 선언
    <details>
        <summary>#!/bin/bash</summary>
        <p>Bash 셸 스크립트</p>
    </details>
    <details>
        <summary>#!/bin/sh</summary>
        <p>POSIX 호환 셸 스크립트</p>
    </details>
    <details>
        <summary>#!/usr/bin/env python3</summary>
        <p>파이썬 스크립트</p>
    </details>
---

## 프로세스
- 프로세스는 실행 중인 프로그램을 의미하며, 리눅스에서 중요한 개념입니다.

- 프로세스 상태
    <details>
        <summary>Running (R)</summary>
        <p>실행 중인 프로세스</p>
    </details>
    <details>
        <summary>Sleeping (S)</summary>
        <p>대기 중인 프로세스</p>
    </details>
      <details>
        <summary>D (Uninterruptible Sleep)</summary>
        <p>인터럽트 불가 대기 (예: I/O 대기 중)</p>
    </details>
    <details>
        <summary>Stopped (T)</summary>
        <p>중지된 프로세스</p>
    </details>
    <details>
        <summary>Zombies (Z)</summary>
        <p>종료되었지만 부모 프로세스가 아직 수집하지 않은 프로세스</p>
    </details>

- 프로세스 확인 및 관리 명령어
    <details>
        <summary>ps</summary>
        <p>현재 실행 중인 프로세스 목록을 확인합니다.</p>
    </details>
    <details>
        <summary>top</summary>
        <p>실시간으로 프로세스 상태를 모니터링합니다.</p>
    </details>
    <details>
        <summary>htop</summary>
        <p>top의 대안으로, 더 직관적인 인터페이스를 제공합니다.</p>
    </details>
    <details>
        <summary>kill</summary>
        <p>프로세스를 종료합니다.</p>
    </details>
    <details>
        <summary>killall</summary>
        <p>특정 이름을 가진 모든 프로세스를 종료합니다.</p>
    </details>

- 프로세스 우선순위
    <details>
        <summary>nice</summary>
        <p>프로세스의 우선순위를 조정합니다.</p>
    </details>
    <details>
        <summary>renice</summary>
        <p>실행 중인 프로세스의 우선순위를 변경합니다.</p>
    </details>

- 명령어 사용
    <details>
        <summary>nice -n [값] [명령어]</summary>
        <p>새로운 프로세스를 생성할 때 우선순위를 설정합니다.</p>
    </details>
    <details>
        <summary>renice -n [값] -p [PID]</summary>
        <p>실행 중인 프로세스의 우선순위를 변경합니다.</p>
    </details>
    <details>
        <summary>일반 사용자 사용 가능 범위</summary>
        <p>-19 ~ +19</p>
    </details>
    <details>
        <summary>root 사용자 사용 가능 범위</summary>
        <p>-20 ~ +19</p> 
    </details>

- fork / exec
    <details>
        <summary>fork</summary>
        <p>현재 프로세스를 복제하여 새로운 프로세스를 생성합니다.</p>
        <p>새로운 프로세스는 부모 프로세스의 메모리 공간을 복사합니다.</p>
    </details>
    <details>
        <summary>exec</summary>
        <p>현재 프로세스의 메모리 공간을 새로운 프로그램으로 대체합니다.</p>
        <p>fork로 만든 자식 프로세스에서 주로 사용</p>
        <p>새로운 프로그램이 실행되며, 기존 프로세스는 종료됩니다.</p>
    </details>