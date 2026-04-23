---
title: PR-255
type: source
status: active
updated: 2026-04-23
tags:
  - wiki
  - source
  - pr
  - history
  - snapshot
source_kind: pr
source_ref: PR-255
commit: 8985b770c8d5297c09a06caa860ae9507c148ab9
---

# PR-255 history refresh dedup and snapshot fix

## 문서 목적
이 문서는 merge commit `8985b77`에서 확인한 `#255` 관련 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#255` |
| Commit | `8985b770c8d5297c09a06caa860ae9507c148ab9` |
| Date | `2026-04-22` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `fix: 새로고침 시 히스토리 결과 중복 및 스냅샷 표시 오류 수정 (#255)`이다.
- 변경 파일은 `backend/src/modules/history/history.controller.ts`, `frontend/src/features/gameplay/history/hooks/useCanvasHistory.ts`, `frontend/src/features/gameplay/history/model/history.types.ts`, `frontend/src/features/gameplay/round/components/RoundSummaryModal.tsx`를 포함한다.
- 백엔드 history controller와 프런트엔드 history hook/type, round summary modal이 함께 수정됐다.
- 커밋 제목 기준으로 페이지 새로고침 이후 history 결과 중복과 snapshot 표시 오류를 보정한 작업이다.

## 관련 문서
- [[wiki/05-Sources/prs/PR-238-timeline-based-history-panel|PR-238]]
- [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]]
- [[wiki/04-Records/Worklog/WK-2026-04-22-01-history-timeline-and-canvas-polish|WK-2026-04-22-01]]
