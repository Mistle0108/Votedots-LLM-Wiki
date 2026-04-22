---
title: PR-157
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - ui
  - countdown
source_kind: pr
source_ref: PR-157
commit: 5f0316d18f78682271265aa4cf7eca76e8ab8700
---

# PR-157 phase-based gameplay ui and countdown

## 문서 목적
이 문서는 merge commit `5f0316d`에서 확인한 `#157` 관련 구현 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#157` |
| Commit | `5f0316d18f78682271265aa4cf7eca76e8ab8700` |
| Date | `2026-04-08` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: align phase-based gameplay ui and countdown flow (#157)`이다.
- 변경 파일은 `backend/src/modules/canvas/canvas.controller.ts`, `frontend/src/features/gameplay/canvas/model/canvas.types.ts`, `frontend/src/features/gameplay/round/components/RoundInfo.tsx`, `frontend/src/features/gameplay/round/model/round.types.ts`, `frontend/src/features/gameplay/session/hooks/useGameplayBootstrap.ts`, `frontend/src/features/gameplay/session/model/session.types.ts`, `frontend/src/features/gameplay/vote/components/VotePanel.tsx`, `frontend/src/features/gameplay/vote/components/VotePopup.tsx`, `frontend/src/pages/canvas/CanvasPage.tsx`, `frontend/src/pages/canvas/model/useCanvasGameplay.ts`, `frontend/src/pages/canvas/model/useCanvasPage.ts`다.
- round info, vote panel/popup, canvas page 모델과 bootstrap이 함께 바뀌며 phase 기반 화면 전환과 countdown 흐름을 맞췄다.
- 변경 범위는 backend controller 일부와 프런트 gameplay UI를 함께 조정해 phase state가 실제 사용자 화면에 반영되게 하는 데 집중돼 있다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow|WK-2026-04-11-01]]
- [[wiki/05-Sources/prs/PR-156-gameplay-bootstrap-phase-alignment|PR-156]]
- [[wiki/05-Sources/prs/PR-175-intro-phase|PR-175]]
