---
title: PR-257
type: source
status: active
updated: 2026-04-23
tags:
  - wiki
  - source
  - pr
  - canvas
  - interaction
source_kind: pr
source_ref: PR-257
commit: 7b8b730f7db75657d22b7cd173134d647b4a295a
---

# PR-257 prevent image drag ghost

## 문서 목적
이 문서는 merge commit `7b8b730`에서 확인한 `#257` 관련 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#257` |
| Commit | `7b8b730f7db75657d22b7cd173134d647b4a295a` |
| Date | `2026-04-22` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `fix : 캔버스 및 게임 이미지 드래그 고스트 방지 (#257)`이다.
- 변경 파일은 `CanvasStage.tsx`, `CanvasSurface.tsx`, `MiniMap.tsx`, `IntroCanvasPreview.tsx`, `RoundSummaryModal.tsx`, `GameSummaryModal.tsx`를 포함한다.
- canvas 본화면, 미니맵, intro preview, round/game summary modal까지 이미지 드래그 동작이 일어날 수 있는 UI에 공통 수정이 들어갔다.
- 커밋 제목 기준으로 브라우저 기본 이미지 drag ghost를 막는 interaction polish 작업이다.

## 관련 문서
- [[wiki/05-Sources/repos/votedots-canvas|votedots-canvas]]
- [[wiki/04-Records/Worklog/WK-2026-04-22-01-history-timeline-and-canvas-polish|WK-2026-04-22-01]]
