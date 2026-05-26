---
title: votedots-lobby-room
type: source
status: active
updated: 2026-05-26
tags:
  - wiki
  - source
  - repo
  - lobby
  - room
source_kind: repo-module
source_ref: votedots/main:lobby-room
commit: ca5d4935b181dbd72e4895de5965b91ae7ae5d4a
---

# votedots-lobby-room

## 목적
이 문서는 plaza, lobby, room, guest/member 입장 흐름 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` |
| Verified | `2026-05-26` |

## 확인 사실
- frontend router에는 `/plaza`, `/lobby`, `/room` 페이지가 있다.
- `/play`는 현재 `/plaza`로 redirect되고, 실제 방/광장 진입과 선택은 `LobbyPage`와 `RoomPage` 흐름으로 이어진다.
- `LobbyPage`는 광장 현재 게임, 완성 캔버스, room list, room create/enter modal, guest/member/private room 인증 modal을 함께 조합한다.
- room 기능은 public/private 타입, access code 해석, current room 조회, participant count/list, manage 정보, end game/terminate 흐름을 포함한다.
- private room 생성과 room 종료/강제 종료는 member-only다.
- room list는 socket 이벤트와 연결되어 hidden 상태일 때 refresh 필요 플래그를 남길 수 있다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/pages/lobby/LobbyPage.tsx` | 광장, 완성 캔버스, 방 목록, room 생성/입장과 guest/member 인증 흐름을 조합한다. |
| Frontend | `frontend/src/pages/plaza/PlazaPage.tsx` | 광장 현재 게임 화면 진입점을 제공한다. |
| Frontend | `frontend/src/pages/room/RoomPage.tsx` | room 세션 기반 실제 플레이 진입점을 제공한다. |
| Frontend | `frontend/src/features/room/*` | room API, room create/enter UI, room list socket hook, lifecycle notice, room session context 저장을 담당한다. |
| Frontend | `frontend/src/features/lobby/*` | completed canvas, guest entry, private room member login, mobile tab 상태를 담당한다. |
| Backend | `backend/src/modules/room/*` | room 목록/상세/생성/입장/current 관리/end game/terminate를 담당한다. |
| Backend | `backend/src/entities/room.entity.ts` | room의 기본 schema를 정의한다. |
| Backend | `backend/src/socket/room-list.events.ts` | room list 변경 방송 이벤트를 정의한다. |

## 주요 API 사실
| 엔드포인트 | 사실 |
| --- | --- |
| `GET /rooms` | room 목록을 조회한다. |
| `GET /rooms/config-profiles` | 방 생성 시 선택할 config profile 목록을 조회한다. |
| `GET /rooms/current` | 현재 사용자의 room 컨텍스트를 조회한다. |
| `GET /rooms/current/participants/count` | 현재 room의 participant 수를 조회한다. |
| `GET /rooms/current/participants` | 현재 room 참여자 목록을 조회한다. |
| `GET /rooms/current/manage` | 현재 room 관리 정보를 조회한다. |
| `POST /rooms/current/end-game` | member가 현재 room 게임을 종료한다. |
| `POST /rooms/current/terminate` | member가 현재 room을 강제 종료한다. |
| `POST /rooms/resolve-access-code` | private room access code를 room id로 해석한다. |
| `POST /rooms/:roomId/enter-public` | 공개 room에 입장한다. |
| `GET /rooms/:roomId` | room 상세를 조회한다. |
| `POST /rooms` | member가 room을 생성한다. |
| `POST /rooms/enter` | 인증된 사용자가 room에 입장한다. |

## 연결 문서
- [[wiki/02-Architecture/System-Reference|System Reference]]
- [[wiki/02-Architecture/Data-Flow|Data Flow]]
- [[wiki/05-Sources/repos/votedots-auth-play|votedots-auth-play]]
- [[wiki/05-Sources/repos/votedots-public-surface|votedots-public-surface]]
- [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]]
