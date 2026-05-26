---
title: Operations
type: operations-architecture
status: active
updated: 2026-05-26
tags:
  - wiki
  - architecture
  - operations
---

# Operations

## 역할
이 문서는 실행 검증 결과를 기록하는 문서가 아니라, 운영 아키텍처 구조를 설명하는 문서다.

## 기준
- 코드 기준선: `main@ca5d4935b181dbd72e4895de5965b91ae7ae5d4a`
- 구조 기준 파일: `docker-compose.prod.yml`

## 운영 topology
| 서비스 | 역할 | 비고 |
| --- | --- | --- |
| `nginx` | 외부 ingress와 reverse proxy | `80/443` 공개 진입점 |
| `backend` | 애플리케이션 서버 | 내부 `4000` 포트 사용 |
| `redis` | 캐시/세션/상태 보조 저장소 | compose 내 서비스 |
| `certbot` | 인증서 갱신 보조 | nginx와 함께 운영 |

## 외부 의존성
| 항목 | 설명 |
| --- | --- |
| Postgres | prod compose 안에 포함되지 않고 외부 DB를 전제로 한다. |
| `shared-db-network` | backend가 외부 DB와 연결되기 위한 외부 네트워크다. |
| env 파일 | root / backend / frontend env 구성이 필요하다. |
| storage volume | snapshot / archive 계열 저장 경로가 운영 구조에 영향을 준다. |
| Telegram | analytics rollup 요약 전송에 사용될 수 있다. |

## local 과 prod 구분
- local 개발 구조는 `docker-compose.yml` 기준이다.
- integration test 인프라는 `docker-compose.test.yml` 기준이다.
- 이 문서는 local 실행 방법을 설명하지 않는다.
- 이 문서는 prod 배치 구조와 운영 전제 조건만 다룬다.

## 품질 / 배포 흐름
| 영역 | 사실 | 근거 |
| --- | --- | --- |
| Frontend build | build/dev 전에 `sync:public-pages`로 공개 정적 페이지를 먼저 생성한다. | `frontend/package.json`, `frontend/scripts/generate-public-pages.mjs` |
| Backend build | TypeScript build 후 static asset 복사 스크립트를 실행한다. | `backend/package.json`, `backend/scripts/copy-static-assets.mjs` |
| CI | `develop` 대상 PR에서 lint, unit/integration test, build, coverage를 실행한다. | `.github/workflows/ci.yml` |
| CD | `main` push 또는 수동 실행 시 원격 서버 deploy script를 SSH로 호출한다. | `.github/workflows/deploy.yml` |
| Analytics ops | rollup/cleanup CLI와 Telegram fallback file 처리 스크립트가 있다. | `backend/src/scripts/*`, `backend/scripts/send-analytics-rollup-host.mjs` |

## 이 문서에 없는 것
- 실제 운영 중 상태
- health check 통과 여부
- 실제 secret 값
- 실제 운영 host / 민감 정보

## 관련 문서
- 구조 기준: [[wiki/02-Architecture/System-Reference|System Reference]]
- 현재 상태: [[wiki/03-Status/Current-State|Current State]]
- 다음 작업: [[wiki/03-Status/Next-Work|Next Work]]
- 구조 사실 근거: [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]
- data / infra source: [[wiki/05-Sources/repos/votedots-data-infra|votedots-data-infra]]
- quality / ops source: [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]]
