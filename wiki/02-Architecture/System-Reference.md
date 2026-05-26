---
title: System Reference
type: architecture-reference
status: active
updated: 2026-05-26
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
| `frontend/src/app/router.tsx` | 현재 진입 경로가 landing/public/auth/plaza/lobby/room/mypage로 크게 바뀌었으므로 라우팅부터 확인한다. |
| `frontend/src/pages` | 공개 페이지, lobby/room, gameplay, mypage 등 최상위 사용자 화면 구성이 모인다. |
| `frontend/src/features` | 기능별 UI, API, 상태 연결이 분리돼 있다. |
| `backend/src/app.ts` | 현재 공개/인증/room/gameplay API 진입점을 한 번에 확인할 수 있다. |
| `backend/src/modules` | 공개 surface, room, account, gameplay, analytics 책임이 모인다. |
| `backend/src/database/migrations` | schema/migration 기준이 필요한 경우 후순위로 확인한다. |

## 핵심 기능 기준 모듈
| 모듈 | 설명 | 우선 경로 | source |
| --- | --- | --- | --- |
| `public surface` | locale landing, static info, completed canvas, login board 공개 진입면 | `frontend/src/pages/landing/*`, `frontend/src/pages/info/*`, `backend/src/modules/public-*/*`, `backend/src/modules/login-board/*` | [[wiki/05-Sources/repos/votedots-public-surface|votedots-public-surface]] |
| `lobby / room` | plaza, lobby, room 생성/입장, private/public room 흐름 | `frontend/src/pages/lobby/*`, `frontend/src/features/room/*`, `backend/src/modules/room/*` | [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]] |
| `auth / account / analytics` | guest/member 계정, mypage, 방문 이벤트 수집/집계 | `frontend/src/pages/login/*`, `frontend/src/pages/register/*`, `frontend/src/pages/mypage/*`, `backend/src/modules/auth/*`, `backend/src/modules/mypage/*`, `backend/src/modules/analytics/*` | [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]] |
| `canvas` | 캔버스 렌더링, outline/profile, 대형 캔버스 대응 구조 | `frontend/src`, 관련 backend state/config | [[wiki/05-Sources/repos/votedots-canvas|votedots-canvas]] |
| `round` | 라운드 상태, intro/summary modal, 패널 흐름 | `frontend/src`, `backend/src` | [[wiki/05-Sources/repos/votedots-round-vote|votedots-round-vote]] |
| `history` | summary, snapshot archive, game history panel | `backend/src`, 관련 frontend panel UI | [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]] |
| `auth/play` | 로그인 후 guest/member 세션과 `/play -> /plaza` 진입 흐름 | `frontend/src`, `backend/src` | [[wiki/05-Sources/repos/votedots-auth-play|votedots-auth-play]] |
| `quality / ops` | test, CI/CD, public page sync, 운영 스크립트 | `.github/workflows/*`, `frontend/test/*`, `backend/test/*`, `frontend/scripts/*`, `backend/src/scripts/*` | [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]] |

## 수정 위치 판단 기준
- landing/public pages 수정은 먼저 `frontend/src/pages/landing/*`, `frontend/src/shared/content/*`, `backend/src/modules/public-landing/*`을 본다.
- lobby/room UX 수정은 `frontend/src/pages/lobby/*`, `frontend/src/features/room/*`, `backend/src/modules/room/*`을 본다.
- guest/member 계정과 mypage 수정은 `backend/src/modules/auth/*`, `backend/src/modules/mypage/*`, 대응 frontend page를 함께 본다.
- gameplay UI와 사용성 수정은 먼저 `frontend/src/features/gameplay/*`와 `frontend/src/pages/canvas/*`를 본다.
- 게임 상태, 저장 구조, API/실시간 처리 수정은 `backend/src/modules/*`와 `backend/src/socket/*`을 본다.
- `templateKey` / `profileKey` 정렬 문제는 backend config와 frontend 사용 지점을 함께 본다.
- 배포/테스트/운영 구조는 이 문서보다 [[wiki/02-Architecture/Operations|Operations]]와 [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]]를 먼저 본다.

## 현재 구조 관련 메모
- 사용자 진입면은 `public landing -> login/guest -> lobby/plaza/room -> gameplay -> summary/history -> mypage`로 확장됐다.
- room/plaza와 public landing이 gameplay 바깥의 독립된 상위 축으로 자리 잡았다.
- 대형 캔버스 대응과 snapshot 기반 결과 조회는 유지되면서, 공개 결과/완성 캔버스 탐색 축이 추가됐다.
- 테스트/배포/분석 스크립트가 codebase의 일상적인 읽기 범위에 포함됐다.

## 관련 문서
- 현재 상태: [[wiki/03-Status/Current-State|Current State]]
- 다음 작업: [[wiki/03-Status/Next-Work|Next Work]]
- 흐름 구조: [[wiki/02-Architecture/Data-Flow|Data Flow]]
- 설계/문제/결정 기록: [[wiki/04-Records/README|04-Records]]
- 구조 사실 근거: [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]
