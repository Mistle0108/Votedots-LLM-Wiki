---
title: Current State
type: current-state
status: active
updated: 2026-04-23
tags:
  - wiki
  - status
  - current-state
---

# Current State

## 기준
- 코드 기준: `main@fecd28db8d164c4cbfe2dab72e20df395380321b`
- 구조 사실 근거: [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]
- issue 근거: [[wiki/05-Sources/issues/README|Issue Sources]]

## 완료된 축
| 항목 | 상태 | 메모 |
| --- | --- | --- |
| 인증 및 `/play` 진입 흐름 | DONE | [[wiki/05-Sources/prs/PR-150-play-entry-route-and-auth-gate|PR-150]], [[wiki/05-Sources/prs/PR-156-gameplay-bootstrap-phase-alignment|PR-156]], [[wiki/05-Sources/prs/PR-182-game-entry-and-game-end-observe|PR-182]] 기준으로 `/play` 진입, 인증 gate, gameplay bootstrap 흐름이 연결돼 있다. |
| session / participant 상태 기반 | DONE | [[wiki/05-Sources/prs/PR-117-redis-active-session-management|PR-117]], [[wiki/05-Sources/prs/PR-118-session-based-participant-state|PR-118]], [[wiki/05-Sources/prs/PR-119-participant-count-and-list-api|PR-119]], [[wiki/05-Sources/prs/PR-120-round-participant-count|PR-120]], [[wiki/05-Sources/prs/PR-121-participant-panel-and-usertype-split|PR-121]] 기준으로 active session, participant identity/state, count/list, panel foundation이 존재한다. |
| socket / timer / vote 실시간 기반 | DONE | [[wiki/05-Sources/prs/PR-033-socket-handler|PR-33]], [[wiki/05-Sources/prs/PR-035-round-timer|PR-35]], [[wiki/05-Sources/prs/PR-041-live-vote-broadcast|PR-41]], [[wiki/05-Sources/prs/PR-057-vote-panel-foundation|PR-57]], [[wiki/05-Sources/prs/PR-058-frontend-socket-integration|PR-58]], [[wiki/05-Sources/prs/PR-059-round-ui-foundation|PR-59]] 기준 foundation이 존재한다. |
| 실시간 캔버스 / 라운드 / 투표 흐름 | DONE | [[wiki/05-Sources/prs/PR-151-game-phase-state-structure|PR-151]], [[wiki/05-Sources/prs/PR-153-phase-scheduler|PR-153]], [[wiki/05-Sources/prs/PR-157-phase-based-gameplay-ui-and-countdown|PR-157]], [[wiki/05-Sources/prs/PR-175-intro-phase|PR-175]] 기준으로 phase state, scheduler, countdown, intro phase 골격이 존재한다. |
| round / game summary 조회 | DONE | [[wiki/05-Sources/prs/PR-201-summary-ready-flow|PR-201]], [[wiki/05-Sources/prs/PR-253-game-summary-modal-adjustments|PR-253]] 기준으로 결과 조회 흐름과 종료 통계/modal 보정이 맞물려 있다. |
| snapshot 기반 history 조회와 타임라인 패널 | DONE | [[wiki/05-Sources/prs/PR-210-separate-game-history-panel-from-canvas-page|PR-210]], [[wiki/05-Sources/prs/PR-211-round-snapshot-entity-and-storage-path|PR-211]], [[wiki/05-Sources/prs/PR-213-server-side-round-snapshot-preview-flow|PR-213]], [[wiki/05-Sources/prs/PR-238-timeline-based-history-panel|PR-238]], [[wiki/05-Sources/prs/PR-255-history-refresh-dedup-and-snapshot-fix|PR-255]] 기준 저장/preview 기반 위에 timeline 조회와 refresh 안정화가 반영돼 있다. |
| 대형 캔버스 렌더 / viewport / interaction | DONE | [[wiki/05-Sources/prs/PR-233-sparse-grid-chunk-rendering|PR-233]], [[wiki/05-Sources/prs/PR-240-initial-center-viewport|PR-240]], [[wiki/05-Sources/prs/PR-257-prevent-image-drag-ghost|PR-257]], [[wiki/05-Sources/prs/PR-259-prevent-cell-select-on-zoom-reset|PR-259]] 기준으로 sparse grid + chunk 구조 위에 중앙 viewport와 interaction polish가 반영돼 있다. |
| outline template registry | PARTIAL | [[wiki/05-Sources/prs/PR-172-outline-template-canvas-creation|PR-172]], [[wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log|PR-173]]로 foundation은 들어왔지만 용어와 기준 정렬이 남아 있다. |

## 부분 완료 / 미정리 영역
| 항목 | 상태 | 근거 |
| --- | --- | --- |
| `history` / `intro` / `round` UI 잔여 gap | PARTIAL | [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]], [[wiki/05-Sources/issues/ISSUE-177-round-panel-intro-round-modal|ISSUE-177]], [[wiki/05-Sources/prs/PR-202-intro-phase-guide-modal|PR-202]], [[wiki/05-Sources/prs/PR-238-timeline-based-history-panel|PR-238]], [[wiki/05-Sources/prs/PR-253-game-summary-modal-adjustments|PR-253]], [[wiki/05-Sources/prs/PR-255-history-refresh-dedup-and-snapshot-fix|PR-255]] |
| `templateKey` vs `profileKey` 방향 정렬 | PARTIAL | [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]], [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]], [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]] |
| 핵심 화면 smoke test 범위 | DONE | 핵심 사용자 흐름 기준 smoke test scope 문서가 존재한다. |
| migration / schema source 보강 | DONE | data/infra, schema/entity, summary persistence source까지 기준 커밋 기준으로 정리됐다. |

## 현재 판단
- 프로젝트의 핵심 플레이 흐름은 `auth/session -> /play -> realtime foundation -> phase foundation -> round/vote -> summary/history` 기준으로 문서화돼 있다.
- `#238`, `#240`, `#253`, `#255`, `#257`, `#259` 범위가 반영되면서 history timeline, 중앙 viewport, summary modal, interaction polish가 완료 축으로 이동했다.
- 남아 있는 주요 `Next Work`는 history/intro/round UI 잔여 gap, smoke test 회귀 확인, template/profile 기준 정렬에 가깝다.

## 다음 문서
- 다음 작업: [[wiki/03-Status/Next-Work|Next Work]]
- 구조와 책임 위치: [[wiki/02-Architecture/System-Reference|System Reference]]
- 작업/문제/결정 이력: [[wiki/04-Records/README|04-Records]]

## wiki baseline 메모
- `main@fecd28db8d164c4cbfe2dab72e20df395380321b` 기준으로 핵심 문서 축(`01-Project`, `02-Architecture`, `03-Status`, `04-Records`, `05-Sources`)은 연결된 상태다.
- 앱 동작 기준 주요 반영은 `0abee77..f6d9f3c` 범위에 있고, `7c47bac..fecd28d` 범위는 wiki 사용을 위한 프로젝트 로컬 설정/AGENTS 정리다.
- 현재 `Next Work`에 남아 있는 항목은 문서 구조 공백이 아니라 프로젝트 구현/정렬 과제다.
- 이후 commit 기준으로 상태를 갱신할 때도 `05-Sources -> 02-Architecture -> 03-Status -> 04-Records -> index/log` 순서를 유지한다.
