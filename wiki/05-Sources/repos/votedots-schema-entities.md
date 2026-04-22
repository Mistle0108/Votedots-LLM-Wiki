---
title: votedots-schema-entities
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - repo
  - schema
  - entities
source_kind: repo-module
source_ref: votedots/main:schema-entities
commit: 31d22b3535627b3a0a56ea1cf9e41411475f72fd
---

# votedots-schema-entities

## 목적
이 문서는 migration과 핵심 entity 구조를 기준 커밋 사실로 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `31d22b3535627b3a0a56ea1cf9e41411475f72fd` |
| Verified | `2026-04-21` |

## 확인 파일
- `backend/src/database/migrations/1783000000000-InitialSchemaReset.ts`
- `backend/src/database/data-source.ts`
- `backend/src/entities/canvas.entity.ts`
- `backend/src/entities/vote-round.entity.ts`
- `backend/src/entities/game-summary.entity.ts`
- `backend/src/entities/round-summary.entity.ts`
- `backend/src/entities/round-snapshot.entity.ts`

## migration 기준 사실
- 기준 커밋에서 확인한 migration 파일은 `1783000000000-InitialSchemaReset.ts` 1개다.
- migration은 `uuid-ossp` extension 생성 후 핵심 테이블을 한 번에 만든다.
- 생성 테이블에는 `canvas`, `voter`, `cell`, `vote_round`, `vote_ticket`, `vote`, `game_summary`, `round_summary`, `round_snapshot`가 포함된다.
- `cell(canvas_id, x, y)`, `vote_round(canvas_id, roundNumber)`, `round_snapshot(round_id)`, `round_snapshot(canvas_id, round_number)` 등에 unique/index 제약이 존재한다.
- `game_summary`는 `canvas_id` unique 기준 1:1 구조를 가진다.
- `round_summary`는 `round_id` unique 기준 라운드당 1개 구조를 가진다.

## DataSource 기준 사실
- `AppDataSource`는 PostgreSQL + TypeORM을 사용한다.
- `synchronize: false` 기준이다.
- entities 배열에는 `Canvas`, `Cell`, `Vote`, `VoteRound`, `VoteTicket`, `Voter`, `GameSummary`, `RoundSummary`, `RoundSnapshot`가 등록돼 있다.
- migration 경로는 `src/database/migrations/*.ts`다.

## 핵심 entity 사실
| Entity | 사실 |
| --- | --- |
| `Canvas` | grid 크기, `configProfileKey`, `backgroundAssetKey`, `configSnapshot`, `phase`, `currentRoundNumber`, 시작/종료 시간을 가진다. |
| `VoteRound` | canvas 소속 라운드이며 `roundNumber`, 시작/종료 시각, `isActive`를 가진다. |
| `GameSummary` | canvas 단위 1개 summary이며 전체 라운드/투표/색상/상위 투표자 집계를 가진다. |
| `RoundSummary` | round 단위 1개 summary이며 참가자 수, 총 투표 수, 진행률, 최다 득표 셀, 동점 추첨 수를 가진다. |
| `RoundSnapshot` | round 단위 snapshot 메타데이터이며 `storagePath`, format, width/height, byteSize, capturedAt을 가진다. |

## 구조 해석 없이 바로 쓸 수 있는 결론
- schema 기준 핵심 집계 테이블은 `game_summary`, `round_summary`, `round_snapshot` 3개다.
- 요약/스냅샷은 canvas와 round를 기준으로 분리되어 저장된다.
- 현재 기준 커밋에서는 migration 파일이 1개이므로 schema 초기 구조는 이 파일을 기준으로 본다.

## 관련 문서
- [[wiki/05-Sources/repos/votedots-data-infra|votedots-data-infra]]
- [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]]
- [[wiki/02-Architecture/Operations|Operations]]

