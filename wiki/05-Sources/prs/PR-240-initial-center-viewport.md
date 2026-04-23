---
title: PR-240
type: source
status: active
updated: 2026-04-23
tags:
  - wiki
  - source
  - pr
  - canvas
  - viewport
source_kind: pr
source_ref: PR-240
commit: 79daff105a5a3ace1fff58c8d026fb1ba5d68ba7
---

# PR-240 initial center viewport

## 문서 목적
이 문서는 merge commit `79daff1`에서 확인한 `#240` 관련 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#240` |
| Commit | `79daff105a5a3ace1fff58c8d026fb1ba5d68ba7` |
| Date | `2026-04-21` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: 초기 진입 시 중앙 뷰포트 적용 (#240)`이다.
- 변경 파일은 `CanvasSurface.tsx`, `useCanvasInteraction.ts`, `useCanvasRenderer.ts`, `canvas.render.ts`, `viewport.ts`, `CanvasPage.tsx`, `useCanvasPage.ts`, `useCanvasScene.ts`를 포함한다.
- 변경 범위는 프런트엔드 canvas 렌더/interaction/viewport 모델과 page scene orchestration에 집중돼 있다.
- 커밋 제목과 변경 파일 기준으로 초기 진입 시 viewport를 중앙 기준으로 맞추는 동작이 canvas page 전반에 반영됐다.

## 관련 문서
- [[wiki/05-Sources/repos/votedots-canvas|votedots-canvas]]
- [[wiki/04-Records/Worklog/WK-2026-04-22-01-history-timeline-and-canvas-polish|WK-2026-04-22-01]]
