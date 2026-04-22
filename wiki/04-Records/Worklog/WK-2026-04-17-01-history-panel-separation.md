---
title: WK-2026-04-17-01
type: worklog
status: active
updated: 2026-04-21
tags:
  - wiki
  - records
  - worklog
  - history
  - ui
---

# WK-2026-04-17-01 history panel 분리

## 문서 목적
이 문서는 2026-04-17 시점의 history panel 분리 작업을 기록한다.

## 작업 일시
2026-04-17

## 작업 목적
- canvas page 안에 섞여 있던 history panel 책임을 feature 계층으로 분리한다.
- 이후 history archive / timeline 확장을 page 전체 수정 없이 이어갈 수 있는 구조를 만든다.

## 변경 영역
- `frontend/src/features/gameplay/history/components/GameHistoryPanel.tsx`
- `frontend/src/features/gameplay/history/index.ts`
- `frontend/src/pages/canvas/CanvasPage.tsx`

## 어떻게 진행했는가
- history panel 전용 컴포넌트를 gameplay history feature 아래로 분리했다.
- page 단에서는 history panel 구현 자체보다 조립/연결 책임만 남기는 방향으로 정리됐다.
- 결과적으로 history panel은 이후 issue 기반 확장(`ISSUE-206`, `ISSUE-234`)의 출발점이 되는 구조를 갖게 됐다.

## 발생한 문제
- history UI가 canvas page 내부 책임으로 남아 있으면 archive/timeline 기능을 붙일 때 page 변경 폭이 커진다.

## 추가로 고려할 부분
- panel 구조를 분리했어도 intro 고정, 최신순 timeline, snapshot archive 탐색 UX는 아직 후속 작업으로 남는다.

## 결과
- history panel 분리 자체는 완료됐고, 현재 남은 과제는 분리된 구조 위에 UX와 archive 흐름을 확장하는 일이다.

## 후속 작업
- [[wiki/03-Status/Next-Work|TASK-001]] history panel intro 고정 + 최신순 timeline
- [[wiki/03-Status/Next-Work|TASK-002]] history / intro / round UI gap 정리

## 관련 문서
- [[wiki/05-Sources/prs/PR-210-separate-game-history-panel-from-canvas-page|PR-210]]
- [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]]
- [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]]
