---
title: 02-Architecture
type: architecture
status: active
updated: 2026-04-21
tags:
  - wiki
  - architecture
---

# 02-Architecture

## 역할
이 섹션은 프로젝트의 구조 문서다.  
어느 코드를 먼저 읽어야 하는지, 운영이 어떤 형태로 구성되는지를 설명한다.

## 문서 구성
- [[wiki/02-Architecture/System-Reference|System Reference]] - 코드 구조, 책임, 우선 확인 경로
- [[wiki/02-Architecture/Data-Flow|Data Flow]] - 사용자 흐름과 상태/데이터 이동 구조
- [[wiki/02-Architecture/Smoke-Test-Scope|Smoke Test Scope]] - 핵심 사용자 흐름 기준 smoke test 범위
- [[wiki/02-Architecture/Operations|Operations]] - 운영 아키텍처 구조, 배포 topology, 외부 의존성

## 읽는 기준
- 수정 위치를 찾고 싶으면 `System-Reference`를 먼저 본다.
- 화면과 상태가 어떻게 이어지는지 보려면 `Data-Flow`를 본다.
- 핵심 회귀 범위를 빠르게 확인하려면 `Smoke-Test-Scope`를 본다.
- 운영 배치 구조를 이해하고 싶으면 `Operations`를 본다.
- 현재 상태와 우선순위는 `03-Status`를 본다.
