---
title: votedots-overview
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - repo
  - votedots
source_kind: repo
source_ref: votedots/main
commit: 31d22b3535627b3a0a56ea1cf9e41411475f72fd
---

# votedots-overview

## 문서 목적
이 문서는 `votedots` repo의 `main@31d22b3535627b3a0a56ea1cf9e41411475f72fd` 기준 사실 요약이다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `31d22b3535627b3a0a56ea1cf9e41411475f72fd` |
| Verified | `2026-04-21` |

## 저장소 요약
- 프런트엔드는 React 19 + Vite + React Router 기반 단일 페이지 앱이다.
- 백엔드는 Express 5 + Socket.IO + TypeORM + Redis session 기반 서버다.
- 주요 사용자 경로는 `/login`, `/register`, `/play` 세 가지다.
- `frontend/src/features/gameplay` 아래로 `canvas`, `history`, `intro`, `round`, `session`, `vote` 기능이 분리돼 있다.
- `backend/src/modules` 아래로 `auth`, `canvas`, `game`, `history`, `participant`, `round`, `summary`, `vote` 모듈이 존재한다.

## 주요 디렉터리
```text
frontend/src/
  app/
  features/gameplay/
  pages/
  shared/

backend/src/
  config/
  database/
  entities/
  middlewares/
  modules/
  socket/
```

## 확인한 엔트리포인트
| 계층 | 파일 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/main.tsx` | `App`를 렌더링한다. |
| Frontend | `frontend/src/app/router.tsx` | `/login`, `/register`, `/play` 라우팅을 정의한다. |
| Backend | `backend/src/index.ts` | Express, Socket.IO, Redis session, DB 연결과 `/auth`, `/canvas`, `/canvas/:canvasId/rounds`, `/vote` 라우팅을 연결한다. |

## 확인한 기능
| 영역 | 사실 | 주요 경로 |
| --- | --- | --- |
| 인증 | 회원가입, 로그인, 로그아웃, 현재 사용자 조회 라우팅이 있다. | `backend/src/modules/auth/*` |
| 캔버스 조회 | 현재 캔버스, 체크 범위, 참여자 목록, 게임 요약 조회 API가 있다. | `backend/src/modules/canvas/*` |
| 라운드 관리 | 라운드 시작/종료, 완료 라운드 조회, 라운드 요약과 스냅샷 조회 API가 있다. | `backend/src/modules/round/*` |
| 투표 | 투표 제출, 라운드별 투표 상태 조회, 현재 스코어 조회 API가 있다. | `backend/src/modules/vote/*` |
| 플레이 UI | `CanvasPage`에서 캔버스, 투표 패널, 히스토리 패널, 요약 모달, 인트로 가이드를 조합한다. | `frontend/src/pages/canvas/*` |
| 캔버스 UI | 캔버스 컨테이너, 화면 렌더링, 좌표 이동, 미니맵, 체크 로더가 구현돼 있다. | `frontend/src/features/gameplay/canvas/*` |
| 라운드 / 세션 UI | 라운드 상태, 타이머, 세션 부트스트랩, 소켓 연동, 참여자 상태 관리가 구현돼 있다. | `frontend/src/features/gameplay/round/*`, `frontend/src/features/gameplay/session/*` |
| 히스토리 / 요약 | 라운드 요약, 게임 요약, 스냅샷 URL 기반 히스토리 패널이 있다. | `frontend/src/features/gameplay/history/*`, `backend/src/modules/history/*`, `backend/src/modules/summary/*` |

## 핵심 모듈
| 모듈 | 사실 | 주요 경로 |
| --- | --- | --- |
| `canvas` | 프런트는 캔버스 렌더링, 좌표 이동, 체크 로딩을 담당하고 백엔드는 캔버스 생성/조회와 체크 범위 조회를 담당한다. | `frontend/src/features/gameplay/canvas/*`, `backend/src/modules/canvas/*` |
| `round` | 프런트는 라운드 상태와 타이머를 관리하고 백엔드는 라운드 시작/종료, 결과 집계, 요약/스냅샷 조회를 담당한다. | `frontend/src/features/gameplay/round/*`, `backend/src/modules/round/*` |
| `vote` | 프런트는 투표 UI와 상태 표시를 담당하고 백엔드는 투표 제출과 현재 라운드 집계를 담당한다. | `frontend/src/features/gameplay/vote/*`, `backend/src/modules/vote/*` |
| `history` / `summary` | 백엔드는 스냅샷 저장과 요약 조회를 담당하고 프런트는 히스토리 패널과 요약 화면을 구성한다. | `frontend/src/features/gameplay/history/*`, `backend/src/modules/history/*`, `backend/src/modules/summary/*` |

## 기반 인프라 / 저장 구조
| 항목 | 사실 | 근거 경로 |
| --- | --- | --- |
| DB | PostgreSQL + TypeORM DataSource를 사용한다. `synchronize`는 `false`다. | `backend/src/database/data-source.ts` |
| 세션 | RedisStore 기반 `express-session`을 사용한다. | `backend/src/config/session.ts` |
| 소켓 | Socket.IO 서버를 `backend/src/index.ts`에서 초기화한다. | `backend/src/index.ts` |
| 스냅샷 저장 | 라운드 스냅샷은 `storage/game-history/<year>/<month>/canvas-<id>/round-xxx.png` 규칙으로 저장된다. | `backend/src/modules/history/history-storage.service.ts` |

## 코드에서 확인한 사실 메모
- 프런트엔드 `package.json`에는 `test` 스크립트가 없다.
- 백엔드 `package.json`의 `test` 스크립트는 placeholder error를 출력한다.
- `main` 기준 작업 트리 및 현재 `develop` 브랜치의 미커밋 변경은 이 문서에 포함하지 않았다.
- 사용자별 실행 경로(`execution_path`)는 shared wiki에 기록하지 않고 `raw/repos/*.local.md` 또는 세션 입력으로만 관리한다.
- `dfb53af..31d22b3` 범위에서는 `.github/ISSUE_TEMPLATE/feature-template.md`, `.github/pull-request-template.md`만 변경됐고 애플리케이션 코드 변경은 확인되지 않았다.
