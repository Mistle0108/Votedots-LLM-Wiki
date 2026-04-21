---
title: System Reference
type: architecture-reference
status: active
updated: 2026-04-21
tags:
  - wiki
  - architecture
  - system-reference
---

# System Reference

## 역할
이 문서는 "어느 코드를 먼저 읽어야 하는가"를 설명하는 구조 문서다.

## 우선 확인 경로
| 경로 | 이유 |
| --- | --- |
| `frontend/src` | 사용자 플로우, 화면 상태, 패널/모달 UX가 모이는 핵심 경로 |
| `backend/src` | 게임 상태, 결과 조회, 저장 흐름, API/실시간 처리의 핵심 경로 |
| `backend/src/database/migrations` | schema/migration 기준이 필요한 경우 후순위로 확인 |

## 핵심 기능 기준 모듈
| 모듈 | 설명 | 우선 경로 | source |
| --- | --- | --- | --- |
| `canvas` | 캔버스 렌더링, outline/profile, 대형 캔버스 대응 구조 | `frontend/src`, 관련 backend state/config | [[wiki/05-Sources/repos/votedots-canvas|votedots-canvas]] |
| `round` | 라운드 상태, intro/summary modal, 패널 흐름 | `frontend/src`, `backend/src` | [[wiki/05-Sources/repos/votedots-round-vote|votedots-round-vote]] |
| `history` | summary, snapshot archive, game history panel | `backend/src`, 관련 frontend panel UI | [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]] |
| `auth/play` | 로그인 후 `/play` 진입과 기본 사용자 흐름 | `frontend/src`, `backend/src` | [[wiki/05-Sources/repos/votedots-auth-play|votedots-auth-play]] |

## 수정 위치 판단 기준
- UI와 사용성 수정은 먼저 `frontend/src`를 본다.
- 게임 상태, 저장 구조, API/실시간 처리 수정은 `backend/src`를 본다.
- `templateKey` / `profileKey` 정렬 문제는 backend config와 frontend 사용 지점을 함께 본다.
- 배포/런타임 구조는 이 문서가 아니라 [[wiki/02-Architecture/Operations|Operations]]를 본다.

## 현재 구조 관련 메모
- 히스토리 패널과 intro/round modal UX는 이미 일부 구현되어 있지만 확장 작업이 남아 있다.
- 대형 캔버스 대응을 위해 sparse grid + chunk 렌더링 방향의 기록이 남아 있다.
- snapshot 기반 결과 조회와 summary 흐름은 이미 기록과 source가 존재한다.

## 관련 문서
- 현재 상태: [[wiki/03-Status/Current-State|Current State]]
- 다음 작업: [[wiki/03-Status/Next-Work|Next Work]]
- 흐름 구조: [[wiki/02-Architecture/Data-Flow|Data Flow]]
- 설계/문제/결정 기록: [[wiki/04-Records/README|04-Records]]
- 구조 사실 근거: [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]
