---
title: Smoke Test Scope
type: architecture-test-scope
status: active
updated: 2026-05-26
tags:
  - wiki
  - architecture
  - test
  - smoke-test
---

# Smoke Test Scope

## 역할
이 문서는 기준 커밋에서 최소한 확인해야 하는 핵심 사용자 흐름을 정리한다.  
실행 결과 기록 문서가 아니라, 어디까지를 smoke test 범위로 볼지 정의하는 문서다.

## 기준
- 코드 기준선: `main@ca5d4935b181dbd72e4895de5965b91ae7ae5d4a`
- 구조 근거: [[wiki/02-Architecture/Data-Flow|Data Flow]]

## 핵심 smoke test 시나리오
| ID | 시나리오 | 확인 포인트 |
| --- | --- | --- |
| ST-001 | 공개 landing 진입과 locale 전환 | `/`, `/ko`, `/en`, patches/roadmap, 정적 정보 페이지가 깨지지 않고 연결되는가 |
| ST-002 | member 로그인 또는 guest session 생성 후 `/lobby` 진입 | 인증 후 lobby 진입과 사용자 상태 복원이 이어지는가 |
| ST-003 | lobby에서 plaza 현재 게임 또는 room 입장 | public/private room 진입 분기와 access code 해석이 정상인가 |
| ST-004 | gameplay 화면에서 canvas/round/session 기본 상태 로드 | 기본 화면이 멈추지 않고 viewport와 phase 상태가 함께 보이는가 |
| ST-005 | round active 상태에서 vote submit | 투표 제출과 현재 vote 상태 반영이 이어지는가 |
| ST-006 | round summary / game summary / history 조회 | 요약 modal, history panel, snapshot 진입이 이어지는가 |
| ST-007 | completed canvas detail / final result 다운로드 | 공개 결과 detail과 이미지 다운로드 경로가 정상인가 |
| ST-008 | member mypage 참여 기록 / 통계 조회 | 참여 기록 목록/상세와 통계 조회가 정상인가 |

## 범위 밖
- 픽셀 단위 렌더링 품질 전체 검증
- 부하 테스트
- 운영 환경 health check
- cross-browser 상세 검증

## 관련 문서
- [[wiki/02-Architecture/System-Reference|System Reference]]
- [[wiki/02-Architecture/Data-Flow|Data Flow]]
- [[wiki/03-Status/Current-State|Current State]]
- [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]]
