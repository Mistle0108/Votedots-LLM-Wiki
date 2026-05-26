---
title: votedots-overview
type: source
status: active
updated: 2026-05-26
tags:
  - wiki
  - source
  - repo
  - votedots
source_kind: repo
source_ref: votedots/main
commit: ca5d4935b181dbd72e4895de5965b91ae7ae5d4a
---

# votedots-overview

## 문서 목적
이 문서는 `votedots` repo의 `main@ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` 기준 사실 요약이다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` |
| Verified | `2026-05-26` |

## 저장소 요약
- 프런트엔드는 React 19 + Vite + React Router 기반 단일 페이지 앱이다.
- 백엔드는 Express 5 + Socket.IO + TypeORM + Redis session 기반 서버다.
- 공개 사용자 경로는 `/`, `/ko`, `/en`, `/{locale}/patches`, `/{locale}/roadmap`, `/{locale}/terms`, `/{locale}/privacy`, `/{locale}/community`, `/{locale}/contact`다.
- 앱 사용자 경로는 `/login`, `/register`, `/play`, `/plaza`, `/lobby`, `/room`, `/mypage`다.
- `/play`는 현재 `/plaza`로 redirect된다.
- `frontend/src/features/gameplay` 아래로 `canvas`, `history`, `intro`, `round`, `session`, `vote` 기능이 분리돼 있다.
- `frontend/src/features` 아래에 `landing`, `room`, `mypage`, `login-board`, `analytics`, `canvas-result` 기능이 추가돼 있다.
- `backend/src/modules` 아래로 `auth`, `analytics`, `canvas`, `history`, `login-board`, `mypage`, `participant`, `public-canvas`, `public-landing`, `room`, `round`, `summary`, `vote` 모듈이 존재한다.
- 프런트/백엔드 모두 Vitest 기반 테스트 스크립트가 있고, GitHub Actions CI/CD 워크플로가 존재한다.

## 주요 디렉터리
```text
frontend/src/
  app/
  features/
  features/gameplay/
  pages/
  shared/
  test/

backend/src/
  config/
  database/
  entities/
  middlewares/
  modules/
  scripts/
  socket/

.github/workflows/
docker-compose*.yml
```

## 확인한 엔트리포인트
| 계층 | 파일 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/main.tsx` | `App`를 렌더링한다. |
| Frontend | `frontend/src/app/router.tsx` | locale landing, public updates, auth, plaza/lobby/room/mypage, static info 라우팅을 정의한다. |
| Backend | `backend/src/app.ts` | Express, CORS, Redis session과 `/auth`, `/analytics`, `/canvas`, `/mypage`, `/public/*`, `/rooms`, `/vote` 라우팅을 연결한다. |
| Backend | `backend/src/index.ts` | runtime env를 로드하고 Redis/DB 연결 재시도와 서버 부팅을 시작한다. |

## 확인한 기능
| 영역 | 사실 | 주요 경로 |
| --- | --- | --- |
| 공개 랜딩 | locale별 landing, patches/roadmap, terms/privacy/community/contact 정적 공개 페이지가 있다. | `frontend/src/pages/landing/*`, `frontend/src/pages/info/*`, `frontend/scripts/generate-public-pages.mjs` |
| 인증 / 계정 | guest session, 회원가입 약관/연령 동의, 로그인/로그아웃, 비밀번호 변경, 회원 탈퇴, 현재 사용자 조회가 있다. | `backend/src/modules/auth/*`, `frontend/src/pages/login/*`, `frontend/src/pages/register/*` |
| plaza / lobby / room | 광장 현재 게임, 완성 캔버스, 방 목록, 공개/비공개 방 생성/입장, private access code 해석, room 종료/강제 종료 흐름이 있다. | `frontend/src/pages/lobby/*`, `frontend/src/features/room/*`, `backend/src/modules/room/*` |
| 플레이 UI | `CanvasPage`에서 캔버스, 투표 패널, 히스토리 패널, 라운드/게임 summary, 튜토리얼과 인트로 가이드를 조합한다. | `frontend/src/pages/canvas/*` |
| 캔버스 UI | 캔버스 렌더링, 모바일 입력 보정, viewport, 미니맵, interaction guard, 결과 다운로드 연결이 구현돼 있다. | `frontend/src/features/gameplay/canvas/*`, `frontend/src/shared/hooks/useSnapshotDownload.ts` |
| 라운드 / 투표 / 세션 | phase sync, bootstrap, room/plaza session 정리, 투표 도구와 설정, 라운드 요약 UI가 있다. | `frontend/src/features/gameplay/round/*`, `frontend/src/features/gameplay/session/*`, `frontend/src/features/gameplay/vote/*`, `backend/src/modules/round/*`, `backend/src/modules/vote/*` |
| 히스토리 / 결과 자산 | 라운드 스냅샷, 게임 summary, timeline history, 공개 final result 다운로드 흐름이 있다. | `frontend/src/features/gameplay/history/*`, `frontend/src/features/canvas-result/*`, `backend/src/modules/history/*`, `backend/src/modules/public-canvas/*`, `backend/src/modules/summary/*` |
| 마이페이지 | 참여 기록 목록/상세, 통계 요약, 계정 관리 UI가 있다. | `frontend/src/pages/mypage/*`, `backend/src/modules/mypage/*` |
| 방문 통계 / 운영 | visit event 수집, 일별 rollup, Telegram 전송 fallback, CI/CD 워크플로가 있다. | `frontend/src/features/analytics/*`, `backend/src/modules/analytics/*`, `backend/src/scripts/*`, `.github/workflows/*` |

## 핵심 모듈
| 모듈 | 사실 | 주요 경로 |
| --- | --- | --- |
| `public surface` | 공개 랜딩, completed canvas, 로그인 보드, static info 페이지를 담당한다. | `frontend/src/pages/landing/*`, `frontend/src/features/landing/*`, `frontend/src/features/login-board/*`, `backend/src/modules/public-landing/*`, `backend/src/modules/public-canvas/*`, `backend/src/modules/login-board/*` |
| `auth` / `account` | guest/member 인증, 약관/연령 동의, 탈퇴, mypage 통계와 참여 기록을 담당한다. | `frontend/src/pages/login/*`, `frontend/src/pages/register/*`, `frontend/src/pages/mypage/*`, `backend/src/modules/auth/*`, `backend/src/modules/mypage/*` |
| `lobby` / `room` | 방 목록, 생성/입장, private room 접근, current room 관리와 참여자 상태를 담당한다. | `frontend/src/pages/lobby/*`, `frontend/src/features/room/*`, `backend/src/modules/room/*` |
| `canvas` | 프런트는 캔버스 렌더링, 좌표 이동, 체크 로딩을 담당하고 백엔드는 캔버스/광장 조회와 체크 범위 조회를 담당한다. | `frontend/src/features/gameplay/canvas/*`, `backend/src/modules/canvas/*` |
| `round` / `vote` / `session` | 프런트는 phase 동기화, 라운드 상태, 투표 도구를 관리하고 백엔드는 라운드 집계와 투표 반영을 담당한다. | `frontend/src/features/gameplay/round/*`, `frontend/src/features/gameplay/session/*`, `frontend/src/features/gameplay/vote/*`, `backend/src/modules/round/*`, `backend/src/modules/vote/*` |
| `history` / `summary` | 백엔드는 스냅샷 저장, final result 자산, 요약 조회를 담당하고 프런트는 history panel과 결과 modal을 구성한다. | `frontend/src/features/gameplay/history/*`, `frontend/src/features/canvas-result/*`, `backend/src/modules/history/*`, `backend/src/modules/public-canvas/*`, `backend/src/modules/summary/*` |
| `quality` / `ops` | 테스트, CI/CD, public page sync, analytics rollup 운영 스크립트를 담당한다. | `frontend/test/*`, `backend/test/*`, `.github/workflows/*`, `frontend/scripts/*`, `backend/src/scripts/*` |

## 기반 인프라 / 저장 구조
| 항목 | 사실 | 근거 경로 |
| --- | --- | --- |
| DB | PostgreSQL + TypeORM DataSource를 사용한다. `synchronize`는 `false`다. | `backend/src/database/data-source.ts` |
| 세션 | RedisStore 기반 `express-session`을 사용한다. | `backend/src/config/session.ts` |
| 소켓 | Socket.IO 서버를 `backend/src/server.ts`에서 만들고 room list / gameplay 이벤트에 사용한다. | `backend/src/server.ts`, `backend/src/socket/*` |
| 스냅샷 저장 | 라운드 스냅샷은 `storage/game-history/<year>/<month>/canvas-<id>/round-xxx.png` 규칙으로 저장된다. | `backend/src/modules/history/history-storage.service.ts` |
| 테스트 인프라 | backend integration test는 `docker-compose.test.yml`의 Postgres/Redis를 전제로 한다. | `docker-compose.test.yml`, `backend/test/integration/helpers/*` |
| 배포 | `main` push 시 GitHub Actions CD가 원격 서버의 `/opt/votedots/deploy/deploy.sh`를 실행한다. | `.github/workflows/deploy.yml` |

## 코드에서 확인한 사실 메모
- 프런트엔드 `package.json`에는 `sync:public-pages`, `test:unit`, `test:integration`, `test:coverage` 스크립트가 있다.
- 백엔드 `package.json`에는 `test:integration`, `analytics:rollup`, `analytics:cleanup`, `migration:*` 스크립트가 있다.
- `main` 기준 작업 트리 및 현재 `develop` 브랜치의 미커밋 변경은 이 문서에 포함하지 않았다.
- 사용자별 실행 경로(`execution_path`)는 shared wiki에 기록하지 않고 `raw/repos/*.local.md` 또는 세션 입력으로만 관리한다.
- `fecd28d..ca5d493` 범위에서는 public landing, room/lobby 시스템, guest/member 계정 확장, mypage, analytics, 테스트/배포 체계가 대거 추가됐다.
