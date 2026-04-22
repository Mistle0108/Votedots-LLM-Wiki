---
title: WK-2026-04-14-02
type: worklog
status: active
updated: 2026-04-21
tags:
  - wiki
  - records
  - worklog
  - intro
  - modal
---

# WK-2026-04-14-02 intro guide modal 연결

## 문서 목적
이 문서는 2026-04-14 시점의 intro phase 안내 모달 추가 작업을 기록한다.

## 작업 일시
2026-04-14

## 작업 목적
- intro phase에서 게임 안내를 전용 modal로 보여주고, canvas page 흐름과 연결한다.
- 이후 round intro / round modal UI 확장의 기반을 만든다.

## 변경 영역
- `frontend/src/features/gameplay/intro/components/IntroCanvasPreview.tsx`
- `frontend/src/features/gameplay/intro/components/IntroGuideModal.tsx`
- `frontend/src/features/gameplay/intro/index.ts`
- `frontend/src/pages/canvas/CanvasPage.tsx`
- `frontend/src/pages/canvas/model/useCanvasGameplay.ts`
- `frontend/src/pages/canvas/model/useCanvasPage.ts`

## 어떻게 진행했는가
- intro feature 아래에 preview / guide modal 컴포넌트를 추가했다.
- canvas page와 page-level hook이 함께 수정돼 intro phase UI가 gameplay page lifecycle에 연결됐다.
- 결과적으로 intro UI는 별도 feature 계층을 가지게 되었고, 이후 round panel / intro / modal gap 정리의 기반이 생겼다.

## 발생한 문제
- intro 안내 UI가 page 흐름과 분리돼 있으면 phase 전환과 사용자 안내 타이밍이 어긋나기 쉽다.

## 추가로 고려할 부분
- intro modal 추가만으로 round panel / round modal 전체 흐름이 완성되지는 않는다.
- `ISSUE-177` 기준의 라운드 진행 패널과 intro/round modal 통합은 후속 정리가 더 필요하다.

## 결과
- intro phase 안내 모달과 관련 preview UI는 도입됐다.

## 후속 작업
- [[wiki/03-Status/Next-Work|TASK-002]] history / intro / round UI gap 정리

## 관련 문서
- [[wiki/05-Sources/prs/PR-202-intro-phase-guide-modal|PR-202]]
- [[wiki/05-Sources/issues/ISSUE-177-round-panel-intro-round-modal|ISSUE-177]]
- [[wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow|WK-2026-04-11-01]]
