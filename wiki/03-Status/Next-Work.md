---
title: Next Work
type: next-work
status: active
updated: 2026-04-21
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
| TASK-001 | 히스토리 패널을 intro 고정 + 최신순 타임라인 구조로 확장 | 현재 가장 사용자 체감이 큰 미완료 UX 구간 | [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]], [[wiki/05-Sources/prs/PR-210-separate-game-history-panel-from-canvas-page|PR-210]] | `PLANNED` |
| TASK-002 | `history` / `intro` / `round` UI 잔여 gap 정리 | session/realtime/phase foundation 위에 남아 있는 화면 차이를 좁혀야 한다 | [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]], [[wiki/05-Sources/issues/ISSUE-177-round-panel-intro-round-modal|ISSUE-177]], [[wiki/05-Sources/prs/PR-120-round-participant-count|PR-120]], [[wiki/05-Sources/prs/PR-121-participant-panel-and-usertype-split|PR-121]], [[wiki/05-Sources/prs/PR-156-gameplay-bootstrap-phase-alignment|PR-156]], [[wiki/05-Sources/prs/PR-157-phase-based-gameplay-ui-and-countdown|PR-157]], [[wiki/05-Sources/prs/PR-175-intro-phase|PR-175]], [[wiki/05-Sources/prs/PR-202-intro-phase-guide-modal|PR-202]], [[wiki/05-Sources/prs/PR-210-separate-game-history-panel-from-canvas-page|PR-210]], [[wiki/05-Sources/prs/PR-211-round-snapshot-entity-and-storage-path|PR-211]], [[wiki/05-Sources/prs/PR-213-server-side-round-snapshot-preview-flow|PR-213]] | `PLANNED` |
| TASK-003 | `templateKey`와 `profileKey` 기준 정렬 | 용어와 기준 진실이 어긋나면 이후 구현이 흔들린다 | [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]], [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]], [[wiki/05-Sources/prs/PR-172-outline-template-canvas-creation|PR-172]], [[wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log|PR-173]], [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]] | `PLANNED` |

## 보류
- 장기 backlog 성격의 항목은 [[wiki/05-Sources/issues/ISSUE-036-todo-backlog|ISSUE-036]] 기준으로 별도 관리한다.

## 작업 후 반영 순서
1. `04-Records`에 작업/문제/결정 기록
2. `Current-State` 반영
3. 후속 작업이 있으면 `Next-Work` 갱신
