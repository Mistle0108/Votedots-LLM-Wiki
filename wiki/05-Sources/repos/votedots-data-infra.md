---
title: votedots-data-infra
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - repo
  - data
  - infra
source_kind: repo-module
source_ref: votedots/main:data-infra
commit: 31d22b3535627b3a0a56ea1cf9e41411475f72fd
---

# votedots-data-infra

## 목적
이 문서는 DB, session, storage, runtime dependency 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `31d22b3535627b3a0a56ea1cf9e41411475f72fd` |
| Verified | `2026-04-21` |

## 확인 사실
- backend는 PostgreSQL + TypeORM DataSource를 사용한다.
- DataSource 설정은 `synchronize: false` 기준이다.
- session은 RedisStore 기반 `express-session`을 사용한다.
- Socket.IO 서버 초기화는 `backend/src/index.ts`에서 수행된다.
- snapshot storage 경로 규칙은 `storage/game-history/<year>/<month>/canvas-<id>/round-xxx.png` 형식이다.
- prod compose는 `nginx`, `backend`, `redis`, `certbot`을 포함하고, Postgres는 외부 의존성이다.
- prod 구조는 외부 `shared-db-network`를 전제로 한다.
- root / backend / frontend env 구성이 필요하다.

## 주요 경로
| 영역 | 경로 | 사실 |
| --- | --- | --- |
| DB 설정 | `backend/src/database/data-source.ts` | PostgreSQL + TypeORM DataSource와 `synchronize: false` 기준이 있다. |
| Migration | `backend/src/database/migrations/*` | schema 변경 이력은 migration 폴더 기준으로 관리된다. |
| Session | `backend/src/config/session.ts` | RedisStore 기반 session 설정이 존재한다. |
| Runtime 진입점 | `backend/src/index.ts` | Express, Socket.IO, session, DB 연결 초기화가 모인다. |
| Storage | `backend/src/modules/history/history-storage.service.ts` | snapshot storage 경로 규칙이 존재한다. |
| Prod topology | `docker-compose.prod.yml` | `nginx`, `backend`, `redis`, `certbot`, 외부 DB/network 전제가 있다. |

## 아직 얕은 부분
- migration 파일별 변경 범위 요약은 아직 없다.
- entity 단위 source 문서는 아직 없다.
- summary 저장 구조를 entity/migration 기준으로 분해한 source는 아직 없다.

## 관련 문서
- [[wiki/02-Architecture/Operations|Operations]]
- [[wiki/03-Status/Current-State|Current State]]
- [[wiki/03-Status/Next-Work|Next Work]]
- [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]

