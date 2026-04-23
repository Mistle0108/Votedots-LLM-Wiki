---
title: Next Work
type: next-work
status: active
updated: 2026-04-23
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
| TASK-001 | `history` / `intro` / `round` UI 잔여 gap 정리 | history timeline과 summary modal 보정까지 들어왔으니, 남아 있는 화면 연결 차이를 마무리해야 한다 | [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]], [[wiki/05-Sources/issues/ISSUE-177-round-panel-intro-round-modal|ISSUE-177]], [[wiki/05-Sources/prs/PR-202-intro-phase-guide-modal|PR-202]], [[wiki/05-Sources/prs/PR-238-timeline-based-history-panel|PR-238]], [[wiki/05-Sources/prs/PR-253-game-summary-modal-adjustments|PR-253]], [[wiki/05-Sources/prs/PR-255-history-refresh-dedup-and-snapshot-fix|PR-255]] | `PLANNED` |
| TASK-002 | history / summary / canvas 핵심 회귀 smoke test 정착 | refresh, viewport, drag, summary 수정이 이어진 만큼 사용자 흐름 기준 회귀 확인 절차를 고정해야 한다 | [[wiki/02-Architecture/Smoke-Test-Scope|Smoke Test Scope]], [[wiki/04-Records/Issues/ISS-002-automation-test-gap|ISS-002]], [[wiki/05-Sources/prs/PR-240-initial-center-viewport|PR-240]], [[wiki/05-Sources/prs/PR-255-history-refresh-dedup-and-snapshot-fix|PR-255]], [[wiki/05-Sources/prs/PR-257-prevent-image-drag-ghost|PR-257]], [[wiki/05-Sources/prs/PR-259-prevent-cell-select-on-zoom-reset|PR-259]] | `PLANNED` |
| TASK-003 | `templateKey`와 `profileKey` 기준 정렬 | 용어와 기준 진실이 어긋나면 이후 구현이 흔들린다 | [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]], [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]], [[wiki/05-Sources/prs/PR-172-outline-template-canvas-creation|PR-172]], [[wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log|PR-173]], [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]] | `PLANNED` |

## 보류
- 장기 backlog 성격의 항목은 [[wiki/05-Sources/issues/ISSUE-036-todo-backlog|ISSUE-036]] 기준으로 별도 관리한다.

## 작업 후 반영 순서
1. `04-Records`에 작업/문제/결정 기록
2. `Current-State` 반영
3. 후속 작업이 있으면 `Next-Work` 갱신
