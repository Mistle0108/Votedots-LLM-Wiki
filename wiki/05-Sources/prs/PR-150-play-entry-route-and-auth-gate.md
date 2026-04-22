---
title: PR-150
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - play
  - auth
source_kind: pr
source_ref: PR-150
commit: 120ab36f6bd3de16391f23dbed4dd4f20abd9c1f
---

# PR-150 /play 진입 경로와 비로그인 접근 제한

## 문서 목적
이 문서는 merge commit `120ab36`에서 확인한 `#150` 관련 구현 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#150` |
| Commit | `120ab36f6bd3de16391f23dbed4dd4f20abd9c1f` |
| Date | `2026-04-07` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `fix: 게임 진입 경로를 /play로 변경하고 비로그인 접근을 제한 (#150)`이다.
- 변경 파일은 `frontend/src/app/router.tsx`, `frontend/src/features/gameplay/session/hooks/useGameSession.ts`, `frontend/src/pages/canvas/CanvasPage.tsx`, `frontend/src/pages/canvas/model/useCanvasGameplay.ts`, `frontend/src/pages/canvas/model/useCanvasPage.ts`, `frontend/src/pages/login/LoginPage.tsx`다.
- 라우터와 로그인 페이지, gameplay session hook, canvas page 모델 계층이 함께 바뀌었다.
- 변경 범위는 `/play`를 게임 진입 경로로 고정하고 비로그인 접근을 막는 인증 gate를 프런트엔드 진입 흐름에 반영하는 데 집중돼 있다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow|WK-2026-04-11-01]]
- [[wiki/05-Sources/repos/votedots-auth-play|votedots-auth-play]]
- [[wiki/05-Sources/prs/PR-182-game-entry-and-game-end-observe|PR-182]]
