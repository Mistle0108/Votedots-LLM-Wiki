---
title: WK-2026-03-23-01
type: worklog
status: active
updated: 2026-04-21
tags:
  - wiki
  - records
  - worklog
  - socket
  - round
  - vote
---

# WK-2026-03-23-01 realtime socket / round / vote foundation

## 문서 목적
이 문서는 2026-03-21부터 2026-03-23까지 backend socket handler, round timer, vote broadcast, frontend socket/vote/round UI foundation이 어떻게 쌓였는지 기록한다.

## 작업 일시
2026-03-21 ~ 2026-03-23

## 작업 목적
- backend에 socket handler와 round timer를 도입한다.
- vote 상태와 round 진행을 실시간 이벤트로 연결한다.
- 프런트엔드에 socket client와 vote/round UI foundation을 만든다.

## 변경 영역
- `backend/src/index.ts`
- `backend/src/socket/*`
- `backend/src/modules/game/game.timer.ts`
- `backend/src/modules/canvas/*`
- `backend/src/modules/round/*`
- `backend/src/modules/vote/*`
- `frontend/src/hooks/useSocket.ts`
- `frontend/src/lib/socket.ts`
- `frontend/src/api/vote.ts`
- `frontend/src/components/vote/*`
- `frontend/src/pages/CanvasPage.tsx`

## 어떻게 진행했는가
- [[wiki/05-Sources/prs/PR-033-socket-handler|PR-33]]에서 backend socket handler 엔트리포인트를 도입했다.
- [[wiki/05-Sources/prs/PR-035-round-timer|PR-35]]에서 round timer와 canvas 생성 시 timer 자동 시작 흐름을 추가했다.
- [[wiki/05-Sources/prs/PR-041-live-vote-broadcast|PR-41]]에서 vote controller/service에 실시간 투표 현황 브로드캐스트를 추가했다.
- [[wiki/05-Sources/prs/PR-057-vote-panel-foundation|PR-57]]에서 frontend vote API와 vote panel foundation을 만들었다.
- [[wiki/05-Sources/prs/PR-058-frontend-socket-integration|PR-58]]에서 frontend socket client/hook을 canvas page에 연결했다.
- [[wiki/05-Sources/prs/PR-059-round-ui-foundation|PR-59]]에서 round info와 vote panel이 실시간 socket 흐름 위에 올라가도록 정리했다.

## 발생한 문제
- backend socket entrypoint와 frontend socket lifecycle이 함께 정리되지 않으면 vote/round 상태가 서로 다른 시점으로 보일 수 있다.
- round timer와 vote broadcast가 분리돼 있으면 사용자 화면에서 현재 round 단계와 투표 가능 상태가 쉽게 어긋난다.

## 추가로 고려한 부분
- 초기 foundation 단계에서는 socket/timer/vote/round UI를 먼저 잇고, 이후 participant/phase/history 정렬은 뒤에서 확장하는 편이 구조적으로 안정적이다.
- 나중의 phase scheduler와 gameplay bootstrap 정렬은 이 realtime foundation을 교체한 것이 아니라, 더 높은 단계에서 재구성한 것으로 봐야 한다.

## 결과
- 현재 코드의 실시간 gameplay 기반은 socket handler, round timer, vote broadcast, frontend socket integration, round/vote UI foundation 위에 서 있다.
- 이후 `PR-153`, `PR-157`, `PR-182`는 이 realtime foundation을 phase, countdown, game_end 관측 기준으로 재정렬한 흐름으로 볼 수 있다.

## 후속 작업
- foundation 자체는 완료로 보되, 이후 구조화는 [[wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow|WK-2026-04-11-01]]에서 이어진다.

## 관련 문서
- [[wiki/05-Sources/prs/PR-033-socket-handler|PR-33]]
- [[wiki/05-Sources/prs/PR-035-round-timer|PR-35]]
- [[wiki/05-Sources/prs/PR-041-live-vote-broadcast|PR-41]]
- [[wiki/05-Sources/prs/PR-057-vote-panel-foundation|PR-57]]
- [[wiki/05-Sources/prs/PR-058-frontend-socket-integration|PR-58]]
- [[wiki/05-Sources/prs/PR-059-round-ui-foundation|PR-59]]
- [[wiki/05-Sources/prs/PR-153-phase-scheduler|PR-153]]
