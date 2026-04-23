---
title: Smoke Test Scope
type: architecture-test-scope
status: active
updated: 2026-04-23
tags:
  - wiki
  - architecture
  - test
  - smoke-test
---

# Smoke Test Scope

## 역할
이 문서는 기준 커밋에서 최소한 확인해야 하는 핵심 사용자 흐름을 정리한다.  
실행 결과 기록 문서가 아니라, 회귀 확인 범위를 정의하는 문서다.

## 기준
- 코드 기준선: `main@fecd28db8d164c4cbfe2dab72e20df395380321b`
- 구조 근거: [[wiki/02-Architecture/Data-Flow|Data Flow]]

## 핵심 smoke test 시나리오
| ID | 시나리오 | 확인 포인트 |
| --- | --- | --- |
| ST-001 | 로그인/회원가입 후 `/play` 진입 | 인증 후 플레이 진입이 이어지는가 |
| ST-002 | `/play`에서 canvas/round/session 기본 상태 로드 | 기본 화면이 깨지지 않고 중앙 viewport와 핵심 상태가 보이는가 |
| ST-003 | round active 상태에서 vote submit | 투표 제출과 현재 vote 상태 반영이 이어지는가 |
| ST-004 | round summary / game summary 조회 | 요약 조회 API와 화면 흐름이 이어지는가 |
| ST-005 | history panel / snapshot 진입 | history timeline 흐름과 snapshot 조회 진입이 이어지는가 |

## 범위 밖
- 픽셀 단위 렌더링 품질 검증
- 부하 테스트
- 운영 환경 health check
- cross-browser 상세 검증

## 관련 문서
- [[wiki/02-Architecture/System-Reference|System Reference]]
- [[wiki/02-Architecture/Data-Flow|Data Flow]]
- [[wiki/03-Status/Current-State|Current State]]
