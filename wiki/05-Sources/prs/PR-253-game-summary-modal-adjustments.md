---
title: PR-253
type: source
status: active
updated: 2026-04-23
tags:
  - wiki
  - source
  - pr
  - summary
  - modal
source_kind: pr
source_ref: PR-253
commit: df3d0f09be34c4d45606b7f07c4a8e704892228f
---

# PR-253 game summary modal adjustments

## 문서 목적
이 문서는 merge commit `df3d0f0`에서 확인한 `#253` 관련 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#253` |
| Commit | `df3d0f09be34c4d45606b7f07c4a8e704892228f` |
| Date | `2026-04-22` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `fix : 게임 종료 통계 수치 및 모달 구성 수정 (#253)`이다.
- 변경 파일은 `backend/src/modules/canvas/canvas.controller.ts`, `backend/src/modules/history/history.service.ts`, `backend/src/modules/summary/summary.service.ts`, `frontend/src/features/gameplay/round/components/RoundSummaryModal.tsx`, `frontend/src/features/gameplay/session/components/GameSummaryModal.tsx`, `frontend/src/features/gameplay/session/api/session.api.ts`를 포함한다.
- 백엔드 summary/history/canvas 조회 경로와 프런트엔드 round/game summary modal 구성이 함께 조정됐다.
- 변경 범위 기준으로 게임 종료 통계 수치 산출과 summary modal 표시 구조를 함께 보정한 작업이다.

## 관련 문서
- [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]]
- [[wiki/04-Records/Worklog/WK-2026-04-22-01-history-timeline-and-canvas-polish|WK-2026-04-22-01]]
