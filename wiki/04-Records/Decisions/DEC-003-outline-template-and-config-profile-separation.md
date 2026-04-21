---
title: DEC-003
type: decision
status: active
updated: 2026-04-21
tags:
  - wiki
  - records
  - decision
  - outline
  - profile
  - canvas
---

# DEC-003 outline template와 config profile 분리

## 문서 목적
이 문서는 canvas 생성에서 outline template와 game config profile을 분리해서 다루는 방향을 기록한다.

## 배경
- outline template는 canvas 모양/배경 자산 선택과 연결된다.
- game config profile은 라운드/진행 규칙과 설정값 묶음으로 다루는 축에 가깝다.
- 두 축을 구분하지 않으면 canvas 생성 메타데이터, 프론트 bootstrap, 이후 template 추가 작업에서 용어와 책임이 섞이기 쉽다.

## 고려한 선택지
- canvas 생성 시 모든 설정을 즉석 계산하고 별도 key를 남기지 않는 방식
- template와 gameplay config를 하나의 key 체계로 묶는 방식
- outline/background 계열과 gameplay profile 계열을 분리하고, canvas 메타데이터에 생성 기준을 남기는 방식

## 최종 결정
- outline/background 계열과 gameplay config profile 계열을 분리해서 다룬다.
- canvas에는 생성 시점 기준의 설정/자산 메타데이터를 남기는 방향으로 간다.

## 결정 이유
- canvas 생성 결과를 나중에 다시 설명하거나 검증하기 쉬워진다.
- profile 파일 분리, migration/entity field 추가, 프론트 bootstrap 정렬을 함께 진행할 수 있다.
- outline template 추가가 반복되더라도 gameplay config와 충돌하지 않게 유지할 수 있다.

## 부작용과 리스크
- `templateKey`와 `profileKey` 용어가 명확히 정리되지 않으면 오히려 혼선이 커질 수 있다.
- 현재 open issue에서도 naming과 기준 진실 정렬이 후속 과제로 남아 있다.

## 영향 범위
- `backend/src/modules/canvas/*`
- `backend/src/config/*`
- `backend/src/database/migrations/*`
- `backend/src/entities/canvas.entity.ts`
- `frontend/src/features/gameplay/session/*`
- `frontend/src/shared/config/game-config.ts`

## 후속 조치
- `templateKey` / `profileKey` 용어와 역할을 하나의 기준으로 정렬한다.
- outline template 추가 작업 시 source of truth를 문서로 같이 남긴다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-10-01-outline-template-and-config-profile|WK-2026-04-10-01]]
- [[wiki/05-Sources/prs/PR-172-outline-template-canvas-creation|PR-172]]
- [[wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log|PR-173]]
- [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]]
- [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]]
