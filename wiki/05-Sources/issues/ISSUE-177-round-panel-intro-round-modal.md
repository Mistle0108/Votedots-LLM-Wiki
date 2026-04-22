---
title: ISSUE-177
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - issue
  - round
  - modal
  - feat
source_kind: issue
source_ref: ISSUE-177
commit: not-applicable
---

# ISSUE-177 라운드 진행 패널 및 인트로/라운드 모달 UI 구현

## 문서 목적
이 문서는 GitHub issue `#177` 본문에서 확인되는 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| Issue Reference | `#177` |
| URL | `https://github.com/Mistle0108/Votedots/issues/177` |
| State | `open` |
| Labels | `feat` |
| Created | `2026-04-11` |
| Updated | `2026-04-17` |
| Body Format | `legacy/custom-feature-template` |

## issue 본문 사실 요약
- 게임 화면 좌측에 라운드 진행 패널을 추가하고, 인트로 및 라운드 항목 클릭 시 모달을 보여주는 UI 구조가 목표로 적혀 있다.
- 전체 라운드 목록 렌더링과 상태 구분, 진행된 항목만 클릭 가능하도록 제어하는 요구가 포함돼 있다.

## issue에 명시된 작업 항목
- 좌측 라운드 진행 패널 레이아웃 추가
- 세로 타임라인형 UI 구성
- 인트로 1개와 전체 라운드 목록 렌더링
- 완료 / 진행 중 / 미진행 상태 구분
- 패널 내부 스크롤 처리
- 인트로 클릭 시 인트로 모달 오픈
- 라운드 클릭 시 라운드 모달 오픈
- 인트로/라운드 타입별 모달 분기 구조 구현
- 초기에는 빈 모달 상태로 구현하고 이후 실제 데이터 연결 가능하게 확장

## issue 본문 메모
- 라운드 모달은 동일한 레이아웃에서 내부 값만 바뀌는 구조를 고려한다고 적혀 있다.
- 데이터 구조 및 조회 방식은 백엔드 서브이슈에서 별도 정리한다고 적혀 있다.

