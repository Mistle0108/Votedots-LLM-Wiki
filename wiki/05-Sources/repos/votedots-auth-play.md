---
title: votedots-auth-play
type: source
status: active
updated: 2026-05-26
tags:
  - wiki
  - source
  - repo
  - auth
  - play
source_kind: repo-module
source_ref: votedots/main:auth-play
commit: ca5d4935b181dbd72e4895de5965b91ae7ae5d4a
---

# votedots-auth-play

## 목적
이 문서는 `votedots` repo의 인증과 `/play -> /plaza` 진입 흐름 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` |
| Verified | `2026-05-26` |

## 확인 사실
- 주요 인증 진입 경로는 `/login`, `/register`다.
- router에서 `/play`는 더 이상 직접 게임 화면을 열지 않고 `/plaza`로 redirect된다.
- frontend router 기준 파일은 `frontend/src/app/router.tsx`다.
- 인증 관련 backend 모듈은 `backend/src/modules/auth/*` 아래에 존재한다.
- backend auth router에는 `guest-session`, `guest-nickname`, `register`, `login`, `logout`, `change-password`, `withdraw`, `me` 엔드포인트가 있다.
- 회원가입은 약관 동의와 만 14세 이상 확인 값을 함께 받는다.
- 로그인 페이지는 guest entry modal을 열 수 있고, guest 세션 생성 성공 시 `/lobby`로 이동한다.
- 회원 전용 기능은 `memberOnlyMiddleware`로 보호되며 mypage, private room 생성/관리, 비밀번호 변경, 탈퇴에 사용된다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/app/router.tsx` | `/login`, `/register`, `/play`, `/plaza`, `/lobby`, `/room`, `/mypage` 라우트를 정의한다. |
| Frontend | `frontend/src/pages/login/*` | member 로그인과 guest 진입 UI가 위치한다. |
| Frontend | `frontend/src/pages/register/*` | username/nickname/password와 약관/연령 동의 기반 회원가입 UI가 위치한다. |
| Frontend | `frontend/src/features/auth/*` | auth API, guest entry scope, validation, logout helper가 위치한다. |
| Frontend | `frontend/src/features/gameplay/session/*` | gameplay bootstrap과 세션 상태 표시 UI가 위치한다. |
| Backend | `backend/src/modules/auth/*` | guest/member 세션, 회원가입/로그인/로그아웃, 탈퇴, 현재 사용자 조회 관련 모듈이 존재한다. |
| Backend | `backend/src/middlewares/auth.middleware.ts` | 인증 여부와 member-only 조건을 판별한다. |

## 연결 문서
- [[wiki/02-Architecture/System-Reference|System Reference]]
- [[wiki/02-Architecture/Data-Flow|Data Flow]]
- [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]]
- [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]]
- [[wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow|WK-2026-04-11-01]]
