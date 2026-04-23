---
title: WK-2026-04-22-01
type: worklog
status: active
updated: 2026-04-23
tags:
  - wiki
  - records
  - worklog
  - history
  - canvas
  - summary
---

# WK-2026-04-22-01 history timeline and canvas polish

## 문서 목적
이 문서는 `main@f6d9f3c`까지 확인한 history timeline, summary modal, canvas viewport/interaction 보정 작업군의 목적과 결과를 기록한다.

## 작업 일시
2026-04-21 ~ 2026-04-22

## 작업 목적
- history panel을 snapshot URL 목록 중심에서 timeline 기반 조회 흐름으로 확장
- 초기 진입 viewport와 zoom/drag interaction을 사용자 기대에 맞게 정렬
- round/game summary modal의 통계 수치와 표시 구성을 보정

## 변경 대상
- `backend/src/modules/history/*`
- `backend/src/modules/summary/*`
- `backend/src/modules/canvas/*`
- `frontend/src/features/gameplay/history/*`
- `frontend/src/features/gameplay/canvas/*`
- `frontend/src/features/gameplay/round/*`
- `frontend/src/features/gameplay/session/*`
- `frontend/src/pages/canvas/*`

## 어떻게 진행했는가
- history 모듈에 controller/service를 추가하고, 프런트엔드에는 history API/hook/type을 도입해 timeline 기반 패널 조회 흐름을 분리했다.
- canvas 진입 시 중앙 viewport를 적용하도록 renderer, interaction, viewport 모델, scene orchestration을 함께 조정했다.
- 게임 종료 통계 수치와 round/game summary modal 구성을 정리하고, 새로고침 시 history 결과 중복과 snapshot 표시 오류를 보정했다.
- canvas, minimap, intro preview, summary modal에 공통으로 이미지 drag ghost 방지와 zoom reset 클릭 가드를 추가했다.

## 발생한 문제
- history panel 분리 이후에도 timeline 탐색, refresh 안정성, snapshot 표시 일관성이 남아 있었다.
- sparse grid + chunk 구조 위에서 viewport 기본 위치와 interaction polish가 부족하면 첫 진입 체감이 어색했다.
- summary modal과 interaction fix는 history/canvas/session 화면을 가로질러 함께 조정해야 했다.

## 결과
- `main@f6d9f3c` 기준으로 history timeline 조회, 초기 중앙 viewport, summary modal 보정, refresh/drag/zoom interaction fix가 코드에 반영돼 있다.
- 기존 `Next Work`의 최우선 항목이던 history timeline 확장 과제는 완료된 작업으로 이동했다.

## 후속 작업
- `history` / `intro` / `round` UI 사이에 남아 있는 화면 gap을 정리해야 한다.
- history, summary, canvas interaction에 대한 핵심 smoke test와 회귀 확인 절차를 보강해야 한다.

## 관련 문서
- [[wiki/05-Sources/prs/PR-238-timeline-based-history-panel|PR-238]]
- [[wiki/05-Sources/prs/PR-240-initial-center-viewport|PR-240]]
- [[wiki/05-Sources/prs/PR-253-game-summary-modal-adjustments|PR-253]]
- [[wiki/05-Sources/prs/PR-255-history-refresh-dedup-and-snapshot-fix|PR-255]]
- [[wiki/05-Sources/prs/PR-257-prevent-image-drag-ghost|PR-257]]
- [[wiki/05-Sources/prs/PR-259-prevent-cell-select-on-zoom-reset|PR-259]]
- [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]]
- [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]]
- [[wiki/02-Architecture/Smoke-Test-Scope|Smoke Test Scope]]
