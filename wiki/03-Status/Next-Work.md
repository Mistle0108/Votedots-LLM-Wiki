---
title: Next Work
type: next-work
status: active
updated: 2026-05-26
tags:
  - wiki
  - status
  - next-work
---

# Next Work

## 우선순위 원칙
- 현재 상태는 [[wiki/03-Status/Current-State|Current State]]를 기준으로 본다.
- 구조 파악은 [[wiki/02-Architecture/System-Reference|System Reference]]를 먼저 확인한다.
- 근거는 [[wiki/05-Sources/README|05-Sources]]를 우선 본다.

## 우선 작업
| ID | 작업 | 이유 | 근거 | 상태 |
| --- | --- | --- | --- | --- |
| TASK-001 | lobby / room / plaza 핵심 회귀 smoke test 정착 | guest/member, public/private room, room lifecycle 분기가 늘어난 만큼 핵심 진입 흐름을 고정된 회귀 절차로 묶어야 한다 | [[wiki/02-Architecture/Smoke-Test-Scope|Smoke Test Scope]], [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]], [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]] | `PLANNED` |
| TASK-002 | public landing / completed preview / 결과 자산 운영 검증 | 공개 진입면과 결과 다운로드가 제품 상위 축이 된 만큼 preview freshness, asset 경로, locale 정적 페이지 sync를 운영 기준으로 점검해야 한다 | [[wiki/05-Sources/repos/votedots-public-surface|votedots-public-surface]], [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]], [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]] | `PLANNED` |
| TASK-003 | analytics rollup / fallback 운영 절차 점검 | visit event가 landing/lobby/room 축까지 확장됐으니 rollup 결과와 Telegram fallback 절차를 실제 운영 관점에서 다시 확인해야 한다 | [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]], [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]] | `PLANNED` |
| TASK-004 | `templateKey`와 `profileKey` 기준 정렬 | 용어와 기준 진실이 어긋나면 room/config/result template 확장 이후 구현이 다시 흔들린다 | [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]], [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]], [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]] | `PLANNED` |

## 보류
- 장기 backlog 성격의 항목은 [[wiki/05-Sources/issues/ISSUE-036-todo-backlog|ISSUE-036]] 기준으로 별도 관리한다.

## 작업 후 반영 순서
1. `04-Records`에 작업/문제/결정 기록
2. `Current-State` 반영
3. 후속 작업이 있으면 `Next-Work` 갱신
