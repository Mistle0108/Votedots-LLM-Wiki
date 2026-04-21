---
title: votedots-auth-play
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - repo
  - auth
  - play
source_kind: repo-module
source_ref: votedots/main:auth-play
commit: 31d22b3535627b3a0a56ea1cf9e41411475f72fd
---

# votedots-auth-play

## 목적
이 문서는 `votedots` repo의 인증과 `/play` 진입 흐름 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `31d22b3535627b3a0a56ea1cf9e41411475f72fd` |
| Verified | `2026-04-21` |

## 확인 사실
- 주요 사용자 진입 경로는 `/login`, `/register`, `/play`다.
- frontend router 기준 파일은 `frontend/src/app/router.tsx`다.
- 인증 관련 backend 모듈은 `backend/src/modules/auth/*` 아래에 존재한다.
- `/play` 진입과 phase 기반 gameplay bootstrap 흐름에 대한 작업 기록이 존재한다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/app/router.tsx` | `/login`, `/register`, `/play` 라우트를 정의한다. |
| Frontend | `frontend/src/pages/canvas/*` | `/play` 이후 주요 화면 진입점이 위치한다. |
| Frontend | `frontend/src/features/gameplay/session/*` | session bootstrap과 상태 표시 관련 UI가 위치한다. |
| Backend | `backend/src/modules/auth/*` | 로그인, 회원가입, 로그아웃, 현재 사용자 조회 관련 모듈이 존재한다. |

## 연결 문서
- [[wiki/02-Architecture/System-Reference|System Reference]]
- [[wiki/02-Architecture/Data-Flow|Data Flow]]
- [[wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow|WK-2026-04-11-01]]

