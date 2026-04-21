---
title: PR-210
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - history
  - ui
source_kind: pr
source_ref: PR-210
commit: f3027bdcd434dd7a9cb6bb31c73eb14a34939805
---

# PR-210 game history panel 분리

## 문서 목적
이 문서는 merge commit `f3027bd`에서 확인한 `#210` 관련 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#210` |
| Commit | `f3027bdcd434dd7a9cb6bb31c73eb14a34939805` |
| Date | `2026-04-17` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: separate game history panel from canvas page (#210)`이다.
- 변경 파일은 `frontend/src/features/gameplay/history/components/GameHistoryPanel.tsx`, `frontend/src/features/gameplay/history/index.ts`, `frontend/src/pages/canvas/CanvasPage.tsx`다.
- `history` feature 영역에 전용 panel 컴포넌트와 export 진입점이 생겼고, `CanvasPage.tsx`가 함께 수정됐다.
- 변경 범위는 백엔드보다 프론트엔드 UI 구조 분리에 집중돼 있다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-17-01-history-panel-separation|WK-2026-04-17-01]]
- [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]]
- [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]]
