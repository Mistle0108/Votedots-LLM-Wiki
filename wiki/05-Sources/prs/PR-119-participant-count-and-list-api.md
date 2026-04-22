---
title: PR-119
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - participant
  - api
source_kind: pr
source_ref: PR-119
commit: e934a51124cef2e84ab551157b9f6ab373877c5d
---

# PR-119 participant count and list API

## 문서 목적
이 문서는 merge commit `e934a51`에서 확인한 `#119` 관련 구현 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#119` |
| Commit | `e934a51124cef2e84ab551157b9f6ab373877c5d` |
| Date | `2026-04-02` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: add current game participant count and list api (#119)`이다.
- 변경 파일은 `backend/src/modules/canvas/canvas.controller.ts`, `backend/src/modules/canvas/canvas.router.ts`, `backend/src/modules/canvas/canvas.service.ts`, `backend/src/modules/participant/participant-session.service.ts`다.
- participant count/list 조회가 canvas API 경로와 participant session service에 함께 연결됐다.
- 변경 범위는 프런트가 현재 게임 참여자 수와 목록을 별도 조회할 수 있게 하는 backend API 기반 추가에 집중돼 있다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-04-01-session-participant-foundation|WK-2026-04-04-01]]
- [[wiki/05-Sources/prs/PR-120-round-participant-count|PR-120]]
- [[wiki/05-Sources/prs/PR-121-participant-panel-and-usertype-split|PR-121]]
