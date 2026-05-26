---
title: Current State
type: current-state
status: active
updated: 2026-05-26
tags:
  - wiki
  - status
  - current-state
---

# Current State

## 기준
- 코드 기준: `main@ca5d4935b181dbd72e4895de5965b91ae7ae5d4a`
- 구조 사실 근거: [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]
- issue 근거: [[wiki/05-Sources/issues/README|Issue Sources]]

## 완료된 축
| 항목 | 상태 | 메모 |
| --- | --- | --- |
| 공개 landing / 정적 페이지 / 완료 캔버스 탐색 | DONE | [[wiki/05-Sources/repos/votedots-public-surface|votedots-public-surface]] 기준으로 locale landing, patches/roadmap, terms/privacy/community/contact, completed canvas 탐색과 공개 결과 다운로드 진입면이 존재한다. |
| guest/member 인증과 `/play -> /plaza` 진입 흐름 | DONE | [[wiki/05-Sources/repos/votedots-auth-play|votedots-auth-play]] 기준으로 guest session, 회원가입 약관/연령 동의, member 로그인, `/play` redirect, member-only 보호 흐름이 존재한다. |
| plaza / lobby / room 기반 플레이 진입 | DONE | [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]] 기준으로 광장 현재 게임, 방 목록, 공개/비공개 방 생성/입장, room lifecycle 관리가 연결돼 있다. |
| 실시간 캔버스 / 라운드 / 투표 / 세션 흐름 | DONE | [[wiki/05-Sources/repos/votedots-canvas|votedots-canvas]], [[wiki/05-Sources/repos/votedots-round-vote|votedots-round-vote]] 기준으로 sparse grid, 모바일 입력 보정, phase sync, vote 도구와 세션 정리가 반영돼 있다. |
| round / game summary / history / 공개 결과 자산 | DONE | [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]], [[wiki/05-Sources/repos/votedots-public-surface|votedots-public-surface]] 기준으로 summary/history, snapshot, final result 다운로드, completed preview 상세 흐름이 존재한다. |
| mypage 참여 기록과 계정 관리 | DONE | [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]] 기준으로 참여 기록 목록/상세, 통계, 비밀번호 변경/탈퇴 기반이 존재한다. |
| 방문 이벤트 수집과 rollup 운영 기반 | DONE | [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]] 기준으로 visit event 수집, retention/rollup, Telegram summary fallback 구조가 존재한다. |
| 테스트 / CI / CD / public page sync 기반 | DONE | [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]] 기준으로 frontend/backend Vitest, integration test compose, develop PR CI, main push CD, 정적 공개 페이지 sync가 존재한다. |

## 부분 완료 / 미정리 영역
| 항목 | 상태 | 근거 |
| --- | --- | --- |
| lobby / room / plaza 회귀 smoke coverage | PARTIAL | [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]], [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]] |
| public landing / completed preview / 결과 자산 운영 검증 | PARTIAL | [[wiki/05-Sources/repos/votedots-public-surface|votedots-public-surface]], [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]] |
| analytics rollup / fallback 운영 검증 | PARTIAL | [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]], [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]] |
| `templateKey` vs `profileKey` 방향 정렬 | PARTIAL | [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]], [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]], [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]] |
| migration / schema와 운영 스크립트 세부 source | DONE | data/infra, schema/entity, summary persistence, quality/ops source까지 기준 커밋 기준으로 정리됐다. |

## 현재 판단
- 프로젝트의 핵심 사용자 흐름은 `public landing -> login/guest -> lobby/plaza/room -> realtime gameplay -> summary/history -> 공개 결과 / mypage` 기준으로 문서화할 수 있는 수준이다.
- `fecd28d..ca5d493` 범위의 큰 변화는 gameplay 내부 보정보다, gameplay 바깥의 공개 surface, room/lobby 시스템, 계정/통계, 품질/운영 축 확장에 가깝다.
- 남아 있는 주요 `Next Work`는 신규 상위 축의 회귀 검증과 운영 정착, 기존 template/profile 기준 정렬에 가깝다.

## 다음 문서
- 다음 작업: [[wiki/03-Status/Next-Work|Next Work]]
- 구조와 책임 위치: [[wiki/02-Architecture/System-Reference|System Reference]]
- 작업/문제/결정 이력: [[wiki/04-Records/README|04-Records]]

## wiki baseline 메모
- `main@ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` 기준으로 핵심 문서 축(`01-Project`, `02-Architecture`, `03-Status`, `05-Sources`)은 public surface, lobby/room, account/analytics, quality/ops까지 포함하도록 확장됐다.
- 이번 갱신은 `fecd28d..ca5d493` 사이에 누락된 현재 브랜치 기능 축을 상태 문서 기준선으로 끌어올리는 성격이다.
- 현재 `Next Work`에 남아 있는 항목은 문서 공백보다 신규 축의 검증/운영 정착 과제에 가깝다.
- 이후 commit 기준으로 상태를 갱신할 때도 `05-Sources -> 02-Architecture -> 03-Status -> 04-Records -> index/log` 순서를 유지한다.
