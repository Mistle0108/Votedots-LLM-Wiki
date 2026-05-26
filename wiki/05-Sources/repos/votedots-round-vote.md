---
title: votedots-round-vote
type: source
status: active
updated: 2026-05-26
tags:
  - wiki
  - source
  - repo
  - round
  - vote
source_kind: repo-module
source_ref: votedots/main:round-vote
commit: ca5d4935b181dbd72e4895de5965b91ae7ae5d4a
---

# votedots-round-vote

## 목적
이 문서는 round 상태와 vote 흐름 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` |
| Verified | `2026-05-26` |

## 확인 사실
- frontend gameplay 기능 아래에 `round`, `vote`, `session` 폴더가 존재한다.
- backend 모듈 아래에 `round`와 `vote` 모듈이 존재한다.
- round 관련 API는 시작/종료, 완료 라운드 조회, round summary와 snapshot 조회를 포함한다.
- vote 관련 API는 투표 제출, 라운드별 투표 상태 조회, 현재 투표 조회를 포함한다.
- frontend에는 phase sync, room/plaza 세션 정리, round summary modal, vote tool/settings, 연속 투표 보조 UI가 존재한다.
- backend vote/round 서비스는 room 기반 플레이와 최근 설정/즉시 투표 상태 보정 흐름과 함께 유지된다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/features/gameplay/round/*` | round 상태, 타이머, intro/summary modal 관련 UI가 위치한다. |
| Frontend | `frontend/src/features/gameplay/vote/*` | vote UI, 도구 선택, settings, 현재 vote 상태 표시가 위치한다. |
| Frontend | `frontend/src/features/gameplay/session/*` | session bootstrap과 참여 상태 연동 UI가 위치한다. |
| Frontend | `frontend/src/pages/canvas/hooks/useGameplayPhaseSync.ts` | phase sync와 gameplay 전환 보조를 담당한다. |
| Backend | `backend/src/modules/round/*` | round 시작/종료, 결과 집계, summary/snapshot 조회 모듈이 위치한다. |
| Backend | `backend/src/modules/vote/*` | vote 제출과 현재 round vote 집계 모듈이 위치한다. |

## 관련 source / 기록
- [[wiki/05-Sources/issues/ISSUE-177-round-panel-intro-round-modal|ISSUE-177]]
- [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]]
- [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]]
- [[wiki/02-Architecture/Data-Flow|Data Flow]]
