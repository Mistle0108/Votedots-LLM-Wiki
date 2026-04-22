---
title: ISSUE-234
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - issue
  - history
  - feat
source_kind: issue
source_ref: ISSUE-234
commit: not-applicable
---

# ISSUE-234 히스토리 패널 구조 개선

## 문서 목적
이 문서는 GitHub issue `#234` 본문에서 확인되는 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| Issue Reference | `#234` |
| URL | `https://github.com/Mistle0108/Votedots/issues/234` |
| State | `open` |
| Labels | `feat` |
| Created | `2026-04-21` |
| Updated | `2026-04-21` |
| Body Format | `.github/ISSUE_TEMPLATE/feature-template.md` |

## issue 본문 사실 요약
- 현재 히스토리 패널은 게임 인트로와 최신 라운드 결과만 제한적으로 보여준다고 적혀 있다.
- 게임 인트로는 항상 상단에 고정하고, 라운드 결과와 최종 게임 결과 통계를 최신순 타임라인으로 표시하도록 구조를 바꾸려는 요청이다.
- 결과 항목 타입은 최소 `round`, `game` 두 가지를 구분하자는 제안이 포함돼 있다.

## issue에 명시된 작업 항목
- 게임 인트로를 히스토리 패널 최상단 고정 섹션으로 유지한다.
- 라운드 결과와 최종 게임 결과를 인트로 아래 공통 히스토리 영역에 표시한다.
- 최신 결과가 항상 위에 오도록 정렬한다.
- 결과 항목에 라운드 번호, 주요 통계, 스냅샷/요약 정보를 표시한다.
- 최종 게임 결과는 일반 라운드 결과와 시각적으로 구분한다.
- 빈 상태 메시지와 자연스러운 패널 스크롤을 요구한다.

## issue 본문 메모
- 추천 구현 방향으로 인트로를 리스트와 분리한 고정 섹션으로 두고, `historyItems` 배열을 앞쪽 삽입 또는 최신순 정렬로 관리하자는 예시가 포함돼 있다.

