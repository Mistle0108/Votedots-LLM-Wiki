---
title: Issue Sources
type: sources-issue-index
status: active
updated: 2026-04-21
tags:
  - wiki
  - sources
  - issues
---

# Issue Sources

## 역할
이 폴더는 GitHub open issue의 사실을 요약한 source 색인이다.

## 현재 상태
- `2026-04-21` 기준 open GitHub issue 6개가 source 문서로 ingest되어 있다.
- 이 폴더는 issue 원문 사실만 다루고, 해석과 판단은 `03-Status`와 `04-Records`로 올린다.

## 템플릿 기준
- issue source 요약은 코드 repo의 `.github/ISSUE_TEMPLATE/*.md` 섹션을 기준으로 한다.
- `bug-report-template.md`: 발생 문제, 재현 절차, 기대 동작/실제 동작, 로그/스크린샷, 발생 환경
- `feature-template.md`: 개요, 목표, 요구사항, 기대 효과, 구현/결정 사항, 완료 조건
- `refactor-template.md`(`Etc`): 작업 이유, Todo

## 반영 규칙
- 새 issue가 생기면 raw 카드와 source 문서를 추가한다.
- 현재 상태 영향이 있으면 [[wiki/03-Status/Current-State|Current State]]에 반영한다.
- 다음 작업 영향이 있으면 [[wiki/03-Status/Next-Work|Next Work]]에 반영한다.

## 현재 문서
- [[wiki/05-Sources/issues/ISSUE-234-history-panel-timeline|ISSUE-234]] - 히스토리 패널 인트로 고정과 최신순 타임라인 요구.
- [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]] - outline template 추가 요청.
- [[wiki/05-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive|ISSUE-206]] - Game History Panel과 snapshot archive 구조.
- [[wiki/05-Sources/issues/ISSUE-177-round-panel-intro-round-modal|ISSUE-177]] - 라운드 패널과 인트로/라운드 모달 UI 요구.
- [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]] - `templateKey` 기반 outline canvas 구조 요구.
- [[wiki/05-Sources/issues/ISSUE-036-todo-backlog|ISSUE-036]] - 장기 backlog 모음.

