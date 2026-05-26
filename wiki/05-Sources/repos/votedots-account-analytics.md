---
title: votedots-account-analytics
type: source
status: active
updated: 2026-05-26
tags:
  - wiki
  - source
  - repo
  - account
  - analytics
source_kind: repo-module
source_ref: votedots/main:account-analytics
commit: ca5d4935b181dbd72e4895de5965b91ae7ae5d4a
---

# votedots-account-analytics

## 목적
이 문서는 계정, mypage, 방문 이벤트 수집/집계 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` |
| Verified | `2026-05-26` |

## 확인 사실
- auth router에는 guest session 생성과 guest nickname 수정, 회원가입/로그인/로그아웃, 비밀번호 변경, 회원 탈퇴, 현재 사용자 조회가 있다.
- schema에는 회원가입 동의, withdrawal, guest flag, mypage summary foundation, visit event 집계 관련 migration이 추가돼 있다.
- mypage는 member-only 페이지이며 참여 기록 목록/상세와 통계 요약을 제공한다.
- frontend는 landing, lobby, plaza, room, guest login, room creation 같은 방문/행동 이벤트를 analytics API로 전송한다.
- backend에는 visit event 수집, retention/rollup, Telegram 요약 전송, fallback message file 처리용 스크립트가 있다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/pages/mypage/MyPage.tsx` | member 전용 mypage UI를 제공한다. |
| Frontend | `frontend/src/features/mypage/*` | mypage API와 타입을 제공한다. |
| Frontend | `frontend/src/features/analytics/*` | 방문 이벤트 payload 생성과 API 호출을 담당한다. |
| Backend | `backend/src/modules/auth/*` | guest/member 세션, 회원가입/로그인/로그아웃, 탈퇴를 담당한다. |
| Backend | `backend/src/modules/mypage/*` | 참여 기록/상세/통계 API를 담당한다. |
| Backend | `backend/src/modules/analytics/*` | 방문 이벤트 수집과 집계 서비스, rate limit validation을 담당한다. |
| Backend | `backend/src/scripts/analytics-rollup.ts` | 일별 방문 이벤트 rollup과 Telegram 전송을 실행한다. |
| Backend | `backend/src/scripts/analytics-cleanup.ts` | retention cleanup를 실행한다. |

## 주요 API 사실
| 엔드포인트 | 사실 |
| --- | --- |
| `POST /auth/guest-session` | guest 세션을 생성한다. |
| `PATCH /auth/guest-nickname` | guest 닉네임을 수정한다. |
| `POST /auth/register` | 회원가입과 약관/연령 동의를 처리한다. |
| `POST /auth/login` | member 로그인을 처리한다. |
| `POST /auth/logout` | 현재 세션을 종료한다. |
| `POST /auth/change-password` | member 비밀번호를 변경한다. |
| `POST /auth/withdraw` | member 탈퇴를 처리한다. |
| `GET /auth/me` | 현재 사용자 정보를 반환한다. |
| `GET /mypage/participations` | 참여 기록 목록을 반환한다. |
| `GET /mypage/participations/:canvasId` | 특정 canvas 참여 상세를 반환한다. |
| `GET /mypage/stats` | mypage 통계를 반환한다. |
| `POST /analytics/events` | 방문 이벤트를 수집한다. |

## 방문 이벤트 사실
- frontend 모델에는 `landing_visit`, `lobby_visit`, `plaza_visit`, `room_visit`, `guest_login`, `public_room_created`, `private_room_created` 이벤트 타입이 존재한다.
- analytics router는 분당 120회 제한 rate limit을 둔다.
- rollup 스크립트는 dry-run/apply 모드와 `--before=` 옵션을 지원한다.

## 연결 문서
- [[wiki/02-Architecture/System-Reference|System Reference]]
- [[wiki/02-Architecture/Operations|Operations]]
- [[wiki/05-Sources/repos/votedots-auth-play|votedots-auth-play]]
- [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]]
- [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]]
