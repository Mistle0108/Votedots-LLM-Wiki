---
title: PR-120
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - participant
  - ui
source_kind: pr
source_ref: PR-120
commit: c044749fb44eac12766d47cfb413962bcce73907
---

# PR-120 round participant count

## 문서 목적
이 문서는 merge commit `c044749`에서 확인한 `#120` 관련 구현 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#120` |
| Commit | `c044749fb44eac12766d47cfb413962bcce73907` |
| Date | `2026-04-04` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: round participant count (#120)`이다.
- 커밋 본문에는 participant count broadcast, real-time participant count in round UI, sync participant count updates in round UI가 포함돼 있다.
- 변경 파일은 backend의 `participant-session.service.ts`, `socket.handler.ts`, `socket.ts`와 frontend의 `RoundInfo.tsx`, `useGameplaySocket.ts`, `useParticipantCount.ts`, `VotePanel.tsx`, `CanvasPage.tsx`, `useCanvasGameplay.ts`, `useCanvasPage.ts` 등이다.
- 변경 범위는 participant count를 socket 기반으로 브로드캐스트하고 round UI에 반영하는 흐름 정리에 집중돼 있다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-04-01-session-participant-foundation|WK-2026-04-04-01]]
- [[wiki/05-Sources/prs/PR-119-participant-count-and-list-api|PR-119]]
- [[wiki/05-Sources/prs/PR-121-participant-panel-and-usertype-split|PR-121]]
