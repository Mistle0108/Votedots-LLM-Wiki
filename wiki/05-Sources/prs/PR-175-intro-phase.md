---
title: PR-175
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - intro
  - phase
source_kind: pr
source_ref: PR-175
commit: c032ef1cb95e4cc98c95679f51f9943c814d68cd
---

# PR-175 intro phase 추가

## 문서 목적
이 문서는 merge commit `c032ef1`에서 확인한 `#175` 관련 구현 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#175` |
| Commit | `c032ef1cb95e4cc98c95679f51f9943c814d68cd` |
| Date | `2026-04-11` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: 게임 시작 intro phase 추가 (#175)`이다.
- 변경 파일은 `backend/src/modules/canvas/canvas.service.ts`, `backend/src/modules/game/game-phase.types.ts`, `backend/src/modules/game/game.timer.ts`, `frontend/src/features/gameplay/round/components/RoundInfo.tsx`, `frontend/src/features/gameplay/session/hooks/useGameplayBootstrap.ts`, `frontend/src/features/gameplay/session/model/game-phase.types.ts`, `frontend/src/features/gameplay/session/model/session.types.ts`, `frontend/src/features/gameplay/vote/components/VotePopup.tsx`, `frontend/src/pages/canvas/model/useCanvasGameplay.ts`다.
- backend timer/service와 frontend gameplay/session/vote UI가 함께 바뀌며 intro phase를 explicit phase로 추가했다.
- 변경 범위는 round 시작 전 단계로 intro를 분리해 이후 intro modal, history intro 고정, round panel 정렬의 기반을 만드는 데 집중돼 있다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow|WK-2026-04-11-01]]
- [[wiki/05-Sources/prs/PR-202-intro-phase-guide-modal|PR-202]]
- [[wiki/05-Sources/issues/ISSUE-177-round-panel-intro-round-modal|ISSUE-177]]
