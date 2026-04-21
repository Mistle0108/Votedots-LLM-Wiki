---
title: votedots-summary-persistence
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - repo
  - summary
  - persistence
source_kind: repo-module
source_ref: votedots/main:summary-persistence
commit: 31d22b3535627b3a0a56ea1cf9e41411475f72fd
---

# votedots-summary-persistence

## 목적
이 문서는 round/game summary와 snapshot 저장 구조를 기준 커밋 사실로 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `31d22b3535627b3a0a56ea1cf9e41411475f72fd` |
| Verified | `2026-04-21` |

## 확인 파일
- `backend/src/modules/summary/summary.service.ts`
- `backend/src/modules/history/round-snapshot.service.ts`
- `backend/src/modules/history/history-storage.service.ts`
- `backend/src/entities/game-summary.entity.ts`
- `backend/src/entities/round-summary.entity.ts`
- `backend/src/entities/round-snapshot.entity.ts`

## summary.service 기준 사실
- `summary.service`는 `Canvas`, `Cell`, `Vote`, `VoteTicket`, `VoteRound`, `RoundSummary`, `GameSummary` repository를 사용한다.
- `getRoundSummary(canvasId, roundId)`는 canvas와 round 기준 `RoundSummary`를 조회한다.
- `getGameSummary(canvasId)`는 canvas 기준 `GameSummary`를 조회한다.
- `saveRoundSummary(canvasId, roundId)`는 vote 목록과 painted cell 수를 읽어 round summary를 저장한다.
- round summary 저장 시 참가자 수, 총 투표 수, painted cell 수, 전체 cell 수, 현재 진행률, 최다 득표 셀, 동점 추첨 수를 계산한다.

## round-snapshot.service 기준 사실
- `buildRoundSnapshotApiPath(canvasId, roundId)`는 `/canvas/{canvasId}/rounds/{roundId}/snapshot` 경로를 사용한다.
- `saveRoundSnapshot`은 canvas와 round 존재를 확인한 뒤 cell 목록을 읽는다.
- outline template은 `backgroundAssetKey` 기준으로 찾아 렌더링에 반영한다.
- PNG 버퍼를 생성한 뒤 storage 경로에 파일을 쓰고, `RoundSnapshot` entity를 upsert한다.

## storage 규칙
- storage root 기본값은 `process.cwd()/storage`다.
- `GAME_HISTORY_STORAGE_ROOT` env가 있으면 그 값을 우선 사용한다.
- snapshot 상대 경로는 `game-history/<year>/<month>/canvas-<id>/round-xxx.png` 형식이다.
- 저장 전 디렉터리를 재귀적으로 생성한다.

## persistence 구조 결론
| 대상 | 저장 단위 | 저장 위치/형식 |
| --- | --- | --- |
| `RoundSummary` | round당 1개 | DB `round_summary` |
| `GameSummary` | canvas당 1개 | DB `game_summary` |
| `RoundSnapshot` | round당 1개 | DB 메타데이터 + 파일 시스템 이미지 |

## 관련 문서
- [[wiki/05-Sources/repos/votedots-schema-entities|votedots-schema-entities]]
- [[wiki/05-Sources/repos/votedots-data-infra|votedots-data-infra]]
- [[wiki/04-Records/Decisions/DEC-002-summary-ready-event-and-snapshot-flow|DEC-002]]

