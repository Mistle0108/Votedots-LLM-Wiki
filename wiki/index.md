---
title: Wiki Index
type: index
status: active
updated: 2026-04-21
tags:
  - wiki
  - index
---

# index

## Core
- [[wiki/Home/README|Home]] - wiki 진입점, 읽는 순서, 핵심 링크.
- [[wiki/Home/Wiki-Operating-Rules|Wiki Operating Rules]] - 팀 공유용 운영 규칙과 LLM 읽기/쓰기 기준.
- [[wiki/Home/Wiki-Usage-Guide|Wiki Usage Guide]] - wiki를 언제 확인하고 언제 갱신할지, LLM 요청 예시 안내.
- [[wiki/01-Project/README|01-Project]] - 프로젝트 목적, 범위, 핵심 흐름과 현재 정의.
- [[wiki/02-Architecture/README|02-Architecture]] - 시스템 구조와 운영 아키텍처 안내.
- [[wiki/03-Status/README|03-Status]] - 현재 상태와 다음 작업 문서 안내.
- [[wiki/04-Records/README|04-Records]] - 작업, 문제, 결정 이력.
- [[wiki/05-Sources/README|05-Sources]] - repo / issue / PR 사실 요약 source 계층.

## Project
- [[wiki/01-Project/README|Project Overview]] - 프로젝트 배경 설명, 범위, 현재 문서 기준.

## Architecture
- [[wiki/02-Architecture/System-Reference|System Reference]] - 코드 위치, 책임, 주요 흐름, 우선 확인 경로.
- [[wiki/02-Architecture/Data-Flow|Data Flow]] - auth/play, round/vote, summary/history 흐름 구조.
- [[wiki/02-Architecture/Smoke-Test-Scope|Smoke Test Scope]] - 핵심 사용자 흐름 기준 smoke test 범위.
- [[wiki/02-Architecture/Operations|Operations]] - 운영 아키텍처 구조, 배포 topology, 외부 의존성.

## Status
- [[wiki/03-Status/Current-State|Current State]] - `main@31d22b3` 기준 완료/부분 완료/미완료 상태.
- [[wiki/03-Status/Next-Work|Next Work]] - 다음 우선 작업과 선행 조건.

## Records
- [[wiki/04-Records/README|Records Home]] - Worklog / Issues / Decisions 진입점.
- [[wiki/04-Records/Worklog/README|Worklog]] - 작업 수행 이력.
- [[wiki/04-Records/Worklog/WK-2026-04-21-01-sparse-grid-chunk-rendering|WK-2026-04-21-01]] - sparse grid + chunk 렌더 구조 전환 기록.
- [[wiki/04-Records/Worklog/WK-2026-04-18-01-round-snapshot-storage-preview|WK-2026-04-18-01]] - round snapshot 저장/preview 기반 기록.
- [[wiki/04-Records/Worklog/WK-2026-04-17-01-history-panel-separation|WK-2026-04-17-01]] - history panel 분리 기록.
- [[wiki/04-Records/Worklog/WK-2026-04-14-02-intro-guide-modal|WK-2026-04-14-02]] - intro guide modal 연결 기록.
- [[wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow|WK-2026-04-11-01]] - `/play`, phase state, scheduler, intro foundation 정리.
- [[wiki/04-Records/Worklog/WK-2026-04-10-01-outline-template-and-config-profile|WK-2026-04-10-01]] - outline template와 config profile 도입 기록.
- [[wiki/04-Records/Worklog/WK-2026-04-04-01-session-participant-foundation|WK-2026-04-04-01]] - session / participant foundation 정리.
- [[wiki/04-Records/Worklog/WK-2026-03-23-01-realtime-socket-round-vote-foundation|WK-2026-03-23-01]] - realtime socket / round / vote foundation 정리.
- [[wiki/04-Records/Issues/README|Issues]] - 구조적 문제와 원인 분석.
- [[wiki/04-Records/Decisions/README|Decisions]] - 설계/기술 선택 근거.
- [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]] - outline template와 config profile 분리 결정.

## Sources
- [[wiki/05-Sources/repos/README|Repo Sources]] - repo overview와 module-level source 진입.
- [[wiki/05-Sources/repos/votedots-overview|votedots-overview]] - `main@31d22b3` 기준 repo 구조와 구현 사실 요약.
- [[wiki/05-Sources/repos/votedots-auth-play|votedots-auth-play]] - 인증과 `/play` 진입 흐름 source.
- [[wiki/05-Sources/repos/votedots-canvas|votedots-canvas]] - canvas 조회와 렌더링 source.
- [[wiki/05-Sources/repos/votedots-round-vote|votedots-round-vote]] - round 상태와 vote 흐름 source.
- [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]] - summary, history, snapshot source.
- [[wiki/05-Sources/repos/votedots-data-infra|votedots-data-infra]] - data source, session, storage, prod dependency source.
- [[wiki/05-Sources/repos/votedots-schema-entities|votedots-schema-entities]] - migration과 핵심 entity 구조 source.
- [[wiki/05-Sources/repos/votedots-summary-persistence|votedots-summary-persistence]] - round/game summary와 snapshot 저장 구조 source.
- [[wiki/05-Sources/issues/README|Issue Sources]] - open issue source 진입.
- [[wiki/05-Sources/prs/README|PR Sources]] - 핵심 merged PR source 진입.
- [[wiki/05-Sources/prs/PR-210-separate-game-history-panel-from-canvas-page|PR-210]] - history panel을 canvas page에서 분리.
- [[wiki/05-Sources/prs/PR-211-round-snapshot-entity-and-storage-path|PR-211]] - round snapshot entity와 storage path 구성.
- [[wiki/05-Sources/prs/PR-213-server-side-round-snapshot-preview-flow|PR-213]] - server-side snapshot preview 흐름 추가.
- [[wiki/05-Sources/prs/PR-202-intro-phase-guide-modal|PR-202]] - intro phase guide modal 추가.
- [[wiki/05-Sources/prs/PR-175-intro-phase|PR-175]] - intro phase 추가.
- [[wiki/05-Sources/prs/PR-157-phase-based-gameplay-ui-and-countdown|PR-157]] - phase 기반 gameplay UI와 countdown 정렬.
- [[wiki/05-Sources/prs/PR-156-gameplay-bootstrap-phase-alignment|PR-156]] - gameplay bootstrap과 participant state를 phase 기준으로 정렬.
- [[wiki/05-Sources/prs/PR-153-phase-scheduler|PR-153]] - backend game flow를 phase scheduler 중심으로 재구성.
- [[wiki/05-Sources/prs/PR-151-game-phase-state-structure|PR-151]] - game phase state structure foundation 추가.
- [[wiki/05-Sources/prs/PR-150-play-entry-route-and-auth-gate|PR-150]] - `/play` 진입 경로와 비로그인 접근 제한.
- [[wiki/05-Sources/prs/PR-121-participant-panel-and-usertype-split|PR-121]] - participant panel과 usertype 구분 UI 추가.
- [[wiki/05-Sources/prs/PR-120-round-participant-count|PR-120]] - participant count broadcast와 round UI 반영.
- [[wiki/05-Sources/prs/PR-119-participant-count-and-list-api|PR-119]] - participant count/list API 추가.
- [[wiki/05-Sources/prs/PR-118-session-based-participant-state|PR-118]] - 세션 기반 participant state 추가.
- [[wiki/05-Sources/prs/PR-117-redis-active-session-management|PR-117]] - Redis active session management 추가.
- [[wiki/05-Sources/prs/PR-059-round-ui-foundation|PR-59]] - round UI foundation 추가.
- [[wiki/05-Sources/prs/PR-058-frontend-socket-integration|PR-58]] - frontend socket integration 추가.
- [[wiki/05-Sources/prs/PR-057-vote-panel-foundation|PR-57]] - vote panel foundation 추가.
- [[wiki/05-Sources/prs/PR-041-live-vote-broadcast|PR-41]] - 실시간 vote broadcast 추가.
- [[wiki/05-Sources/prs/PR-035-round-timer|PR-35]] - round timer foundation 추가.
- [[wiki/05-Sources/prs/PR-033-socket-handler|PR-33]] - backend socket handler foundation 추가.
- [[wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log|PR-173]] - canvas config profile과 outline template 메타데이터 정리.
- [[wiki/05-Sources/prs/PR-172-outline-template-canvas-creation|PR-172]] - outline template 정의와 canvas 생성 적용.

## Special
- [[wiki/index|index]] - 전체 문서 카탈로그.
- [[wiki/log|log]] - ingest, query, update, structure change 이력.
