---
title: PR Sources
type: sources-pr-index
status: active
updated: 2026-04-21
tags:
  - wiki
  - sources
  - prs
---

# PR Sources

## 목적
이 디렉터리는 핵심 merged PR의 구현 사실을 요약하는 source 계층이다.

## 기준
- raw PR 카드와 merge commit에서 확인 가능한 최소 사실만 기록한다.
- 제목, 날짜, 변경 범위, 관련 문서를 중심으로 정리한다.
- 설계 해석과 선택 이유는 `04-Records`에서 다룬다.

## 템플릿 기준
- PR source 요약은 코드 repo의 `.github/pull-request-template.md` 섹션을 기준으로 본다.
- 관련 이슈(`Close #...`)
- 개요
- 작업 범위 및 변경 파일
- 테스트 확인 항목

## 현재 문서
- [[wiki/05-Sources/prs/PR-233-sparse-grid-chunk-rendering|PR-233]] - sparse grid + chunk 렌더링 구조 전환.
- [[wiki/05-Sources/prs/PR-210-separate-game-history-panel-from-canvas-page|PR-210]] - history panel을 canvas page에서 feature 영역으로 분리.
- [[wiki/05-Sources/prs/PR-211-round-snapshot-entity-and-storage-path|PR-211]] - round snapshot entity와 storage path 구성 추가.
- [[wiki/05-Sources/prs/PR-213-server-side-round-snapshot-preview-flow|PR-213]] - server-side round snapshot preview 흐름 추가.
- [[wiki/05-Sources/prs/PR-202-intro-phase-guide-modal|PR-202]] - intro phase 안내 modal과 preview UI 추가.
- [[wiki/05-Sources/prs/PR-201-summary-ready-flow|PR-201]] - summary ready 이벤트 기반 결과 조회 복구.
- [[wiki/05-Sources/prs/PR-182-game-entry-and-game-end-observe|PR-182]] - 게임 참여와 GAME_END 관측 흐름 개선.
- [[wiki/05-Sources/prs/PR-175-intro-phase|PR-175]] - intro phase를 explicit phase로 추가.
- [[wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log|PR-173]] - canvas config profile과 outline template 메타데이터 정리.
- [[wiki/05-Sources/prs/PR-172-outline-template-canvas-creation|PR-172]] - outline template 정의와 canvas 생성 적용.
- [[wiki/05-Sources/prs/PR-157-phase-based-gameplay-ui-and-countdown|PR-157]] - phase 기반 gameplay UI와 countdown 정렬.
- [[wiki/05-Sources/prs/PR-156-gameplay-bootstrap-phase-alignment|PR-156]] - gameplay bootstrap과 participant state를 phase 기준으로 정렬.
- [[wiki/05-Sources/prs/PR-153-phase-scheduler|PR-153]] - backend game flow를 phase scheduler 중심으로 재구성.
- [[wiki/05-Sources/prs/PR-151-game-phase-state-structure|PR-151]] - game phase state structure와 phase field foundation 추가.
- [[wiki/05-Sources/prs/PR-150-play-entry-route-and-auth-gate|PR-150]] - `/play` 진입 경로 고정과 비로그인 접근 제한 추가.
- [[wiki/05-Sources/prs/PR-121-participant-panel-and-usertype-split|PR-121]] - participant panel과 usertype 구분 UI 추가.
- [[wiki/05-Sources/prs/PR-120-round-participant-count|PR-120]] - participant count broadcast와 round UI 반영.
- [[wiki/05-Sources/prs/PR-119-participant-count-and-list-api|PR-119]] - participant count/list API 추가.
- [[wiki/05-Sources/prs/PR-118-session-based-participant-state|PR-118]] - 로그인 세션 기반 participant state 관리 추가.
- [[wiki/05-Sources/prs/PR-117-redis-active-session-management|PR-117]] - Redis active session management와 single active session enforcement 추가.
- [[wiki/05-Sources/prs/PR-059-round-ui-foundation|PR-59]] - round info와 vote panel UI foundation 추가.
- [[wiki/05-Sources/prs/PR-058-frontend-socket-integration|PR-58]] - frontend socket integration 추가.
- [[wiki/05-Sources/prs/PR-057-vote-panel-foundation|PR-57]] - vote panel foundation 추가.
- [[wiki/05-Sources/prs/PR-041-live-vote-broadcast|PR-41]] - 실시간 vote broadcast 추가.
- [[wiki/05-Sources/prs/PR-035-round-timer|PR-35]] - round timer foundation 추가.
- [[wiki/05-Sources/prs/PR-033-socket-handler|PR-33]] - backend socket handler foundation 추가.
