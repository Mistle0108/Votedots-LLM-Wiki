---
title: ISSUE-206
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - issue
  - history
  - snapshot
  - feat
source_kind: issue
source_ref: ISSUE-206
commit: not-applicable
---

# ISSUE-206 Game History Panel 및 라운드 스냅샷 아카이브 구조 도입

## 문서 목적
이 문서는 GitHub issue `#206` 본문에서 확인되는 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| Issue Reference | `#206` |
| URL | `https://github.com/Mistle0108/Votedots/issues/206` |
| State | `open` |
| Labels | `feat` |
| Created | `2026-04-17` |
| Updated | `2026-04-17` |
| Body Format | `legacy/custom-feature-template` |

## issue 본문 사실 요약
- 현재 왼쪽 패널은 인트로 가이드와 최신 라운드 결과 진입 정도의 제한적인 역할만 수행한다고 적혀 있다.
- 초기 기획은 인트로 가이드, 각 라운드 결과, 게임 종료 통계를 언제든 다시 확인할 수 있는 사이드 패널 구조였다고 적혀 있다.
- 라운드별 셀 변화 데이터를 직접 누적 저장하는 방식은 비용이 커질 수 있어, 라운드 종료 시 preview 이미지를 생성·저장하는 방향으로 바꾼다고 적혀 있다.
- Game History Panel에서 저장된 라운드 스냅샷을 다시 열어볼 수 있는 구조를 도입하려는 요청이다.

## issue에 명시된 작업 항목
- 기존 왼쪽 영역을 Game History Panel로 재정의한다.
- 라운드 종료 시 서버가 preview 이미지를 생성하고 저장한다.
- 서버 로컬 스토리지와 PostgreSQL 메타데이터 기반 스냅샷 아카이브 구조를 구축한다.
- 프론트가 저장된 스냅샷을 이용해 각 라운드 결과를 다시 표시할 수 있도록 한다.
- 포함 범위는 `CanvasPage`에서 패널 분리, 스냅샷 저장 구조, 셀 데이터 기반 렌더링, 스냅샷 조회 API, 패널 UI 개선이다.

## issue 본문 메모
- 제외 범위로 full 해상도 이미지, 외부 객체 스토리지, diff 기반 재생, contact sheet, 브라우저 로컬 스토리지가 적혀 있다.

