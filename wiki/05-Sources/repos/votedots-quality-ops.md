---
title: votedots-quality-ops
type: source
status: active
updated: 2026-05-26
tags:
  - wiki
  - source
  - repo
  - quality
  - ops
source_kind: repo-module
source_ref: votedots/main:quality-ops
commit: ca5d4935b181dbd72e4895de5965b91ae7ae5d4a
---

# votedots-quality-ops

## 목적
이 문서는 테스트, CI/CD, 공개 페이지 sync, 운영 스크립트 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` |
| Verified | `2026-05-26` |

## 확인 사실
- frontend와 backend 모두 Vitest 기반 test 스크립트를 갖고 있다.
- backend integration test는 별도 Postgres/Redis test compose와 helper runtime을 사용한다.
- CI는 `develop` 대상 pull request에서 lint, unit/integration test, build, coverage를 실행한다.
- CD는 `main` push 또는 수동 실행 시 원격 서버 deploy script를 SSH로 호출한다.
- frontend build/dev는 공개 정적 페이지를 먼저 생성하는 `sync:public-pages` 단계를 선행한다.
- backend에는 analytics rollup/cleanup 운영 스크립트가 있고, build 시 static asset 복사 스크립트를 함께 실행한다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/package.json` | `sync:public-pages`, `test:*`, `build` 스크립트를 정의한다. |
| Frontend | `frontend/test/*` | unit/integration 테스트와 test setup을 포함한다. |
| Frontend | `frontend/vitest.config.ts` | frontend 테스트 구성을 정의한다. |
| Backend | `backend/package.json` | `test:*`, `analytics:*`, `migration:*`, `build` 스크립트를 정의한다. |
| Backend | `backend/test/*` | integration test와 test runtime helper를 포함한다. |
| Backend | `backend/vitest.config.ts` | backend 테스트 구성을 정의한다. |
| Repo | `.github/workflows/ci.yml` | develop PR 기준 CI 단계를 정의한다. |
| Repo | `.github/workflows/deploy.yml` | main push 기준 CD 단계를 정의한다. |
| Repo | `docker-compose.test.yml` | integration test용 Postgres/Redis 구성을 정의한다. |

## 연결 문서
- [[wiki/02-Architecture/Operations|Operations]]
- [[wiki/03-Status/Current-State|Current State]]
- [[wiki/03-Status/Next-Work|Next Work]]
- [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]]
