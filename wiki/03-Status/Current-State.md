---
title: Current State
type: current-state
status: active
updated: 2026-04-21
tags:
  - wiki
  - status
  - current-state
---

# Current State

## 기준
- 코드 기준: `main@31d22b3535627b3a0a56ea1cf9e41411475f72fd`
- 구조 사실 근거: [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]
- issue 근거: [[wiki/05-Sources/issues/README|Issue Sources]]

## 완료된 축
| 항목 | 상태 | 메모 |
| --- | --- | --- |
| 인증 및 `/play` 진입 흐름 | DONE | [[wiki/05-Sources/prs/PR-150-play-entry-route-and-auth-gate|PR-150]], [[wiki/05-Sources/prs/PR-156-gameplay-bootstrap-phase-alignment|PR-156]], [[wiki/05-Sources/prs/PR-182-game-entry-and-game-end-observe|PR-182]] 기준으로 `/play` 진입, 인증 gate, gameplay bootstrap 흐름이 연결돼 있다. |
| session / participant 상태 기반 | DONE | [[wiki/05-Sources/prs/PR-117-redis-active-session-management|PR-117]], [[wiki/05-Sources/prs/PR-118-session-based-participant-state|PR-118]], [[wiki/05-Sources/prs/PR-119-participant-count-and-list-api|PR-119]], [[wiki/05-Sources/prs/PR-120-round-participant-count|PR-120]], [[wiki/05-Sources/prs/PR-121-participant-panel-and-usertype-split|PR-121]] 기준으로 active session, participant identity/state, count/list, panel foundation이 존재한다. |
| socket / timer / vote 실시간 기반 | DONE | [[wiki/05-Sources/prs/PR-033-socket-handler|PR-33]], [[wiki/05-Sources/prs/PR-035-round-timer|PR-35]], [[wiki/05-Sources/prs/PR-041-live-vote-broadcast|PR-41]], [[wiki/05-Sources/prs/PR-057-vote-panel-foundation|PR-57]], [[wiki/05-Sources/prs/PR-058-frontend-socket-integration|PR-58]], [[wiki/05-Sources/prs/PR-059-round-ui-foundation|PR-59]] 기준 foundation이 존재한다. |
| 실시간 캔버스 / 라운드 / 투표 흐름 | DONE | [[wiki/05-Sources/prs/PR-151-game-phase-state-structure|PR-151]], [[wiki/05-Sources/prs/PR-153-phase-scheduler|PR-153]], [[wiki/05-Sources/prs/PR-157-phase-based-gameplay-ui-and-countdown|PR-157]], [[wiki/05-Sources/prs/PR-175-intro-phase|PR-175]] 기준으로 phase state, scheduler, countdown, intro phase 골격이 존재한다. |
| round / game summary 조회 | DONE | summary ready 흐름과 결과 조회 기록이 맞물려 있다. |
| snapshot 기반 history 조회 | DONE | [[wiki/05-Sources/prs/PR-211-round-snapshot-entity-and-storage-path|PR-211]], [[wiki/05-Sources/prs/PR-213-server-side-round-snapshot-preview-flow|PR-213]] 기준 저장/preview 기반이 존재한다. |
| 대형 캔버스 렌더 구조 | DONE | sparse grid + chunk 렌더 방향이 반영돼 있다. |
| outline template registry | PARTIAL | [[wiki/05-Sources/prs/PR-172-outline-template-canvas-creation|PR-172]], [[wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log|PR-173]]로 foundation은 들어왔지만 용어와 기준 정렬이 남아 있다. |

## 부분 완료 / 미정리 영역
| 항목 | 상태 | 근거 |
| --- | --- | --- |
| 히스토리 패널 UX 확장 | PARTIAL | [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]], [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]], [[wiki/05-Sources/prs/PR-210-separate-game-history-panel-from-canvas-page|PR-210]] |
| `templateKey` vs `profileKey` 방향 정렬 | PARTIAL | [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]], [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]], [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]] |
| 핵심 화면 smoke test 범위 | DONE | 핵심 사용자 흐름 기준 smoke test scope 문서가 존재한다. |
| migration / schema source 보강 | DONE | data/infra, schema/entity, summary persistence source까지 기준 커밋 기준으로 정리됐다. |

## 현재 판단
- 프로젝트의 핵심 플레이 흐름은 `auth/session -> /play -> realtime foundation -> phase foundation -> round/vote -> summary/history` 기준으로 문서화돼 있다.
- 기준 커밋 기준 wiki baseline은 near-ready 상태이며, 남아 있는 주요 `Next Work`는 문서 공백보다 프로젝트 구현/정렬 과제에 가깝다.

## 다음 문서
- 다음 작업: [[wiki/03-Status/Next-Work|Next Work]]
- 구조와 책임 위치: [[wiki/02-Architecture/System-Reference|System Reference]]
- 작업/문제/결정 이력: [[wiki/04-Records/README|04-Records]]

## wiki baseline 메모
- `main@31d22b3535627b3a0a56ea1cf9e41411475f72fd` 기준으로 핵심 문서 축(`01-Project`, `02-Architecture`, `03-Status`, `04-Records`, `05-Sources`)은 연결된 상태다.
- 현재 `Next Work`에 남아 있는 항목은 문서 구조 공백이 아니라 프로젝트 구현/정렬 과제다.
- 이후 commit 기준으로 상태를 갱신할 때도 `05-Sources -> 02-Architecture -> 03-Status -> 04-Records -> index/log` 순서를 유지한다.
