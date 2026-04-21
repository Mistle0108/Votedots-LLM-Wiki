---
title: WK-2026-04-10-01
type: worklog
status: active
updated: 2026-04-21
tags:
  - wiki
  - records
  - worklog
  - outline
  - profile
  - canvas
---

# WK-2026-04-10-01 outline template + config profile 기반 정리

## 문서 목적
이 문서는 2026-04-10 시점의 outline template 도입과 canvas config profile 정리 작업을 함께 기록한다.

## 작업 일시
2026-04-10

## 작업 목적
- canvas 생성 시 outline template 선택과 게임 설정 profile을 구조적으로 다룰 수 있게 만든다.
- canvas가 어떤 설정/배경 자산 기준으로 만들어졌는지 메타데이터를 남긴다.

## 변경 영역
- `backend/src/modules/canvas/template/*`
- `backend/src/modules/canvas/canvas.service.ts`
- `backend/src/config/game-config-profiles/*`
- `backend/src/config/game.config.ts`
- `backend/src/database/migrations/1778000000000-AddCanvasConfigFields.ts`
- `backend/src/entities/canvas.entity.ts`
- `frontend/src/features/gameplay/session/*`
- `frontend/src/shared/config/game-config.ts`

## 어떻게 진행했는가
- outline template 데이터/서비스/타입 계층을 canvas 모듈 아래에 추가했다.
- canvas 생성 서비스에 template 적용 흐름을 붙였다.
- game config profile을 파일 단위로 분리하고, canvas 관련 config field를 migration/entity에 반영했다.
- 프론트엔드 session/bootstrap/canvas 타입 계층을 함께 맞춰 profile 기반 설정을 읽을 수 있게 했다.

## 발생한 문제
- template와 profile이 같은 의미인지, 다른 책임인지 용어 기준이 정리되지 않으면 이후 기능 확장에서 혼선이 생긴다.

## 추가로 고려할 부분
- 현재 open issue 기준으로도 `templateKey`와 `profileKey` 용어 정렬이 아직 남아 있다.
- outline template 추가 작업은 앞으로도 반복될 가능성이 높아서, naming과 source of truth를 더 명확히 해야 한다.

## 결과
- outline template 도입과 config profile 기반 설정 구조의 기초는 이 시점에 만들어졌다.

## 후속 작업
- [[wiki/03-Status/Next-Work|TASK-003]] `templateKey`와 `profileKey` 기준 정렬

## 관련 문서
- [[wiki/05-Sources/prs/PR-172-outline-template-canvas-creation|PR-172]]
- [[wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log|PR-173]]
- [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]]
- [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]]
- [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]]
