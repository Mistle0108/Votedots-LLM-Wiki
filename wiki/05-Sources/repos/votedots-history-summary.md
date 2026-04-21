---
title: votedots-history-summary
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - repo
  - history
  - summary
source_kind: repo-module
source_ref: votedots/main:history-summary
commit: 31d22b3535627b3a0a56ea1cf9e41411475f72fd
---

# votedots-history-summary

## 목적
이 문서는 summary, history, snapshot archive 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `31d22b3535627b3a0a56ea1cf9e41411475f72fd` |
| Verified | `2026-04-21` |

## 확인 사실
- frontend gameplay 기능 아래에 `history` 폴더가 존재한다.
- backend 모듈 아래에 `history`와 `summary` 모듈이 존재한다.
- round summary, game summary, snapshot URL 기반 history panel 흐름이 존재한다.
- snapshot 저장 경로 규칙은 `storage/game-history/<year>/<month>/canvas-<id>/round-xxx.png` 형식으로 기록돼 있다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/features/gameplay/history/*` | history panel과 summary 화면 관련 UI가 위치한다. |
| Backend | `backend/src/modules/history/*` | snapshot 저장과 history 조회 관련 모듈이 위치한다. |
| Backend | `backend/src/modules/summary/*` | round/game summary 조회 모듈이 위치한다. |
| Backend | `backend/src/modules/history/history-storage.service.ts` | snapshot 저장 경로 규칙이 기록돼 있다. |

## 관련 source / 기록
- [[wiki/05-Sources/prs/PR-201-summary-ready-flow|PR-201]]
- [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]]
- [[wiki/04-Records/Decisions/DEC-002-summary-ready-event-and-snapshot-flow|DEC-002]]

