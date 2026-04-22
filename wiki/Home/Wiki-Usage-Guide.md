---
title: Wiki Usage Guide
type: wiki-usage-guide
status: active
updated: 2026-04-22
tags:
  - wiki
  - home
  - usage-guide
---

# Wiki Usage Guide

## 목적
- 이 문서는 팀원이 Votedots wiki를 실제로 어떻게 사용해야 하는지 빠르게 안내한다.
- 목적은 아래 3가지를 쉽게 수행하게 하는 것이다.
  - 작업 시작 전에 현재 상태와 다음 작업을 확인하기
  - 작업 완료 후 wiki에 반영이 필요한 내용을 판단하기
  - LLM에게 어떤 방식으로 요청해야 하는지 바로 알기

## 이 wiki에서 먼저 보면 되는 문서
- [[wiki/Home/README|Home]]
  - wiki 진입점, 기준 커밋, 읽는 순서를 확인한다.
- [[wiki/03-Status/Current-State|Current State]]
  - 지금 기준 커밋에서 이미 구현된 상태를 확인한다.
- [[wiki/03-Status/Next-Work|Next Work]]
  - 다음 우선 작업과 남은 gap을 확인한다.
- [[wiki/02-Architecture/System-Reference|System Reference]]
  - 어느 코드 영역을 봐야 하는지 확인한다.
- [[wiki/04-Records/README|04-Records]]
  - 왜 이런 구조와 결정이 되었는지 확인한다.
- [[wiki/05-Sources/README|05-Sources]]
  - repo, issue, PR 근거 문서를 확인한다.

## 언제 wiki를 확인해야 하는가
- 새 작업을 시작하기 전
- 다른 사람이 진행하던 작업을 이어받기 전
- 현재 우선순위와 남은 작업을 다시 확인해야 할 때
- 특정 기능이 왜 그렇게 구현되었는지 배경이 필요할 때
- 관련 코드 위치와 참고 근거 문서를 빠르게 찾아야 할 때

## 언제 wiki를 갱신해야 하는가
- 프로젝트 repo의 기능 PR이 기준 브랜치에 merge된 뒤
- 기준 커밋 기준 현재 상태가 바뀌었을 때
- 다음 우선 작업이나 선행 조건이 바뀌었을 때
- 중요한 문제, 결정, 이력이 새로 생겼을 때
- 새 source 문서나 기록 문서를 추가해야 할 만큼 재사용 가치가 생겼을 때

## LLM에게 현재 상태를 물어보는 방법
- 작업 시작 전에는 아래처럼 요청한다.

```text
wiki 읽고 현재 상태와 다음 작업을 정리해줘.
```

- 특정 영역만 확인하고 싶으면 범위를 같이 적는다.

```text
wiki 읽고 history panel 관련 현재 상태, 남은 작업, 참고할 근거 문서를 정리해줘.
```

- 기대 결과는 아래 4가지다.
  - 현재 완료된 작업
  - 현재 gap이 남아 있는 작업
  - 다음 우선 작업
  - 각 항목의 근거 문서

## LLM에게 작업 완료 후 반영을 요청하는 방법
- 기능 PR이 merge된 뒤에는 아래처럼 요청한다.

```text
프로젝트 main 브랜치 최신 merge commit 기준으로 wiki 반영이 필요한 내용을 정리해줘.
필요한 raw, Sources, Current-State, Next-Work, Records를 갱신해줘.
```

- 특정 merge commit을 기준으로 고정하고 싶으면 commit hash를 같이 준다.

```text
프로젝트 main@<commit> 기준으로 wiki를 갱신해줘.
Current-State, Next-Work, 필요한 Sources/Records까지 반영해줘.
```

- 기대 결과는 아래 순서를 따른다.
  - 기준 branch + commit 확인
  - 필요한 raw/source/status/records 반영
  - 변경 요약 제시
  - 사용자 승인 후 커밋
  - 사용자 승인 후 PR 요청

## 작업 흐름 예시
1. 작업 시작 전에 LLM에게 wiki를 읽고 현재 상태와 다음 작업을 정리해달라고 요청한다.
2. 필요한 경우 `System Reference`, `Data Flow`, `Records`, `Sources`까지 확장해서 읽게 한다.
3. 프로젝트 repo에서 기능 작업과 PR merge가 완료되면, merge commit 기준으로 wiki 반영을 요청한다.
4. LLM이 변경 내용을 요약하면 사람이 검토한다.
5. 사람이 승인하면 wiki repo에 커밋과 PR을 진행한다.
