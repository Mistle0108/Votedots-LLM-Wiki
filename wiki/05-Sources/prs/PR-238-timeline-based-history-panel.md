---
title: PR-238
type: source
status: active
updated: 2026-04-23
tags:
  - wiki
  - source
  - pr
  - history
  - timeline
source_kind: pr
source_ref: PR-238
commit: 0abee7719bf1a234c72740b367caf661ab542d36
---

# PR-238 timeline-based history panel

## 문서 목적
이 문서는 merge commit `0abee77`에서 확인한 `#238` 관련 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#238` |
| Commit | `0abee7719bf1a234c72740b367caf661ab542d36` |
| Date | `2026-04-21` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: 히스토리 패널을 타임라인 기반으로 개선 (#238)`이다.
- 변경 파일에는 `backend/src/modules/history/history.controller.ts`, `backend/src/modules/history/history.service.ts`, `frontend/src/features/gameplay/history/api/history.api.ts`, `frontend/src/features/gameplay/history/hooks/useCanvasHistory.ts`, `frontend/src/features/gameplay/history/components/GameHistoryPanel.tsx`, `frontend/src/features/gameplay/history/model/history.types.ts`가 포함된다.
- 백엔드 history 모듈에 controller/service가 추가돼 히스토리 패널 전용 조회 흐름이 분리됐다.
- 프런트엔드 history 기능에는 API, hook, 타입이 추가됐고 `GameHistoryPanel`과 `CanvasPage` 연계가 함께 수정됐다.
- 커밋 본문에는 canvas initialization order 안정화와 타임라인 항목 overflow scroll 적용이 함께 포함돼 있다.

## 관련 문서
- [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]]
- [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]]
- [[wiki/04-Records/Worklog/WK-2026-04-22-01-history-timeline-and-canvas-polish|WK-2026-04-22-01]]
