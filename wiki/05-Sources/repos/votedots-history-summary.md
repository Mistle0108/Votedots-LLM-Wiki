---
title: votedots-history-summary
type: source
status: active
updated: 2026-04-23
tags:
  - wiki
  - source
  - repo
  - history
  - summary
source_kind: repo-module
source_ref: votedots/main:history-summary
commit: fecd28db8d164c4cbfe2dab72e20df395380321b
---

# votedots-history-summary

## 목적
이 문서는 summary, history, snapshot archive 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `fecd28db8d164c4cbfe2dab72e20df395380321b` |
| Verified | `2026-04-23` |

## 확인 사실
- frontend gameplay 기능 아래에 `history` 폴더가 존재한다.
- backend 모듈 아래에 `history`와 `summary` 모듈이 존재한다.
- round summary, game summary, timeline 기반 history panel 흐름이 존재한다.
- history 모듈에는 timeline 조회를 담당하는 controller/service가 포함된다.
- history refresh 중복과 snapshot 표시 오류 보정, 게임 종료 통계 수치와 summary modal 보정이 반영돼 있다.
- snapshot 저장 경로 규칙은 `storage/game-history/<year>/<month>/canvas-<id>/round-xxx.png` 형식으로 기록돼 있다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/features/gameplay/history/*` | history panel, history hook/API/type, summary 화면 관련 UI가 위치한다. |
| Backend | `backend/src/modules/history/*` | snapshot 저장, timeline history 조회, history controller/service가 위치한다. |
| Backend | `backend/src/modules/summary/*` | round/game summary 조회와 종료 통계 관련 모듈이 위치한다. |
| Backend | `backend/src/modules/history/history-storage.service.ts` | snapshot 저장 경로 규칙이 기록돼 있다. |

## 관련 source / 기록
- [[wiki/05-Sources/prs/PR-201-summary-ready-flow|PR-201]]
- [[wiki/05-Sources/prs/PR-238-timeline-based-history-panel|PR-238]]
- [[wiki/05-Sources/prs/PR-253-game-summary-modal-adjustments|PR-253]]
- [[wiki/05-Sources/prs/PR-255-history-refresh-dedup-and-snapshot-fix|PR-255]]
- [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]]
- [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]]
- [[wiki/04-Records/Decisions/DEC-002-summary-ready-event-and-snapshot-flow|DEC-002]]
