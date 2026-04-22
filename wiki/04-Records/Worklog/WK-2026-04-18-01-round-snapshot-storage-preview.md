---
title: WK-2026-04-18-01
type: worklog
status: active
updated: 2026-04-21
tags:
  - wiki
  - records
  - worklog
  - history
  - snapshot
  - preview
---

# WK-2026-04-18-01 round snapshot 저장/preview 기반 추가

## 문서 목적
이 문서는 2026-04-17~2026-04-18 구간의 round snapshot 저장 및 preview 흐름 도입 작업을 기록한다.

## 작업 일시
2026-04-18

## 작업 목적
- 라운드 종료 결과를 이미지 snapshot으로 저장하고, 이후 history/archive UI에서 다시 읽을 수 있는 기반을 만든다.
- preview 생성과 저장 경로 관리를 서버 기준으로 정리한다.

## 변경 영역
- `backend/src/database/migrations/1780000000000-AddRoundSnapshotTable.ts`
- `backend/src/entities/round-snapshot.entity.ts`
- `backend/src/modules/history/history-storage.service.ts`
- `backend/src/modules/history/round-snapshot-render.service.ts`
- `backend/src/modules/history/round-snapshot.service.ts`
- `backend/src/modules/round/*`
- `frontend/src/features/gameplay/round/*`
- `frontend/src/pages/canvas/model/*`

## 어떻게 진행했는가
- 먼저 snapshot entity, migration, storage path 구성을 추가해 저장 기반을 만들었다.
- 이어서 서버 사이드 render/service와 round API를 연결해 preview 생성 흐름을 붙였다.
- 프론트엔드 round summary modal과 canvas page 훅이 함께 수정돼 snapshot preview를 소비할 수 있는 구조가 생겼다.

## 발생한 문제
- history/archive를 panel UI만으로 확장하면 저장 포맷과 경로, 이미지 생성 기준이 불안정해질 수 있다.

## 추가로 고려할 부분
- snapshot 저장과 preview 생성 기반은 들어왔지만, panel UX와 timeline 구조는 별도 후속 작업이 남아 있다.

## 결과
- history/archive UI가 의존할 수 있는 snapshot 저장/preview 기반이 마련됐다.

## 후속 작업
- [[wiki/03-Status/Next-Work|TASK-001]] history timeline UX 정리
- [[wiki/03-Status/Next-Work|TASK-002]] history / intro / round UI gap 정리

## 관련 문서
- [[wiki/05-Sources/prs/PR-211-round-snapshot-entity-and-storage-path|PR-211]]
- [[wiki/05-Sources/prs/PR-213-server-side-round-snapshot-preview-flow|PR-213]]
- [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]]
- [[wiki/04-Records/Decisions/DEC-002-summary-ready-event-and-snapshot-flow|DEC-002]]
