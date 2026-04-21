---
title: votedots-canvas
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - repo
  - canvas
source_kind: repo-module
source_ref: votedots/main:canvas
commit: 31d22b3535627b3a0a56ea1cf9e41411475f72fd
---

# votedots-canvas

## 목적
이 문서는 canvas 조회와 렌더링 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `31d22b3535627b3a0a56ea1cf9e41411475f72fd` |
| Verified | `2026-04-21` |

## 확인 사실
- frontend gameplay 기능 아래에 `canvas` 기능 폴더가 존재한다.
- backend 모듈 아래에 `canvas` 모듈이 존재한다.
- canvas 관련 API는 현재 canvas, 체크 범위, 참여자 목록, 게임 요약 조회를 포함한다.
- 대형 canvas 대응을 위해 sparse grid + chunk 렌더링 관련 기록과 PR이 존재한다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/features/gameplay/canvas/*` | canvas container, 좌표 이동, 체크 로딩, 미니맵 관련 UI가 위치한다. |
| Frontend | `frontend/src/pages/canvas/*` | CanvasPage에서 canvas UI를 다른 gameplay UI와 조합한다. |
| Backend | `backend/src/modules/canvas/*` | canvas 생성/조회와 체크 범위 조회 관련 모듈이 위치한다. |

## 관련 source / 기록
- [[wiki/05-Sources/prs/PR-233-sparse-grid-chunk-rendering|PR-233]]
- [[wiki/04-Records/Issues/ISS-001-large-canvas-full-grid-bottleneck|ISS-001]]
- [[wiki/04-Records/Decisions/DEC-001-sparse-grid-and-chunk-rendering|DEC-001]]

