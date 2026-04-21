---
title: ISSUE-168
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - issue
  - canvas
  - outline
  - feat
source_kind: issue
source_ref: ISSUE-168
commit: not-applicable
---

# ISSUE-168 템플릿 키 기반 아웃라인 캔버스 생성 구조 도입

## 문서 목적
이 문서는 GitHub issue `#168` 본문에서 확인되는 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| Issue Reference | `#168` |
| URL | `https://github.com/Mistle0108/Votedots/issues/168` |
| State | `open` |
| Labels | `feat` |
| Created | `2026-04-10` |
| Updated | `2026-04-10` |
| Body Format | `legacy/custom-feature-template` |

## issue 본문 사실 요약
- 현재 캔버스는 생성 시 모든 셀이 빈 상태로 초기화된다고 적혀 있다.
- 향후에는 특정 좌표가 미리 검정색으로 칠해진 아웃라인 캔버스를 생성할 수 있어야 한다고 적혀 있다.
- 템플릿 데이터는 서버 DB에 저장하지 않고, 별도 페이지에서 생성한 뒤 `templateKey` 형태의 인코딩된 값으로 전달한다는 방향이 적혀 있다.
- 캔버스 생성과 템플릿 생성 페이지를 분리하는 것이 핵심이라고 적혀 있다.

## issue에 명시된 작업 항목
- 템플릿 생성 전용 페이지 제공
- grid 크기 기준 아웃라인 좌표 선택
- 서버 저장 없이 결과를 `templateKey`로 인코딩
- 캔버스 생성 시 `templateKey` 선택 전달
- 서버 디코드, 키 유효성/크기/좌표 범위 검증
- 아웃라인 좌표 셀을 검정색으로 초기화
- 세부 구현을 하위 이슈로 분리

## issue 본문 메모
- 별도 DB 저장소를 두지 않고, 복사/붙여넣기 가능한 키 기반 데이터로 취급한다고 적혀 있다.
- 상세 구현과 정책 결정은 하위 이슈에서 추가 정의한다고 적혀 있다.

