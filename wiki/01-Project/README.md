---
title: 01-Project
type: project
status: active
updated: 2026-04-21
tags:
  - wiki
  - project
---

# 01-Project

## 한 줄 설명
Votedots는 실시간 캔버스와 라운드 기반 진행을 중심으로 투표와 결과 확인을 수행하는 프로젝트다.

## 이 문서의 역할
- 프로젝트의 목적과 범위를 정의한다.
- 현재 구현 상태의 상세 목록은 적지 않고 `03-Status`로 연결한다.
- 구조와 코드 위치 설명은 `02-Architecture`로 연결한다.

## 현재 문서 기준
- 코드 기준선: `main@31d22b3535627b3a0a56ea1cf9e41411475f72fd`
- 구조 사실 근거: [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]
- 현재 상태: [[wiki/03-Status/Current-State|Current State]]
- 다음 작업: [[wiki/03-Status/Next-Work|Next Work]]

## 핵심 사용자 흐름
1. 인증 후 `/play`로 진입한다.
2. 라운드 상태를 확인하고 캔버스/투표 흐름에 참여한다.
3. 라운드 요약과 게임 요약을 조회한다.
4. 히스토리/스냅샷 기반 결과를 다시 확인한다.

## 현재 프로젝트 범위
| 영역 | 설명 | 문서 |
| --- | --- | --- |
| 인증 및 플레이 진입 | 로그인/회원가입 후 플레이 화면 진입 흐름 | [[wiki/03-Status/Current-State|Current State]] |
| 실시간 캔버스/라운드/투표 | 캔버스 조작, 라운드 상태, 투표 제출과 반영 | [[wiki/02-Architecture/System-Reference|System Reference]] |
| 결과/히스토리 조회 | round/game summary와 snapshot 기반 결과 조회 | [[wiki/05-Sources/repos/votedots-overview|votedots-overview]] |
| 히스토리 UX 확장 | intro 고정, 최신순 타임라인 등 후속 UX 보강 | [[wiki/03-Status/Next-Work|Next Work]] |
| outline/template 방향 정리 | `templateKey` / `profileKey` 기준 정렬 | [[wiki/04-Records/README|04-Records]] |

## 프로젝트 문서 읽기
- 프로젝트 정의는 이 문서를 기준으로 본다.
- 구현 상태는 [[wiki/03-Status/Current-State|Current State]]를 기준으로 본다.
- 구조와 수정 위치는 [[wiki/02-Architecture/System-Reference|System Reference]]를 기준으로 본다.
- 원본 근거는 [[wiki/05-Sources/README|05-Sources]]를 기준으로 본다.

