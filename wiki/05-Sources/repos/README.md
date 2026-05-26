---
title: Repo Sources
type: sources-repo-index
status: active
updated: 2026-05-26
tags:
  - wiki
  - sources
  - repo
---

# Repo Sources

## 역할
이 폴더는 repo 기준 사실 요약을 모은다.  
전체 overview 1개와, 기능 단위로 더 잘게 나눈 module source 문서를 함께 둔다.

## 기준
- repo: `votedots`
- branch: `main`
- commit: `ca5d4935b181dbd72e4895de5965b91ae7ae5d4a`

## 문서 구성
- [[wiki/05-Sources/repos/votedots-overview|votedots-overview]] - repo 전체 구조와 구현 사실 요약
- [[wiki/05-Sources/repos/votedots-auth-play|votedots-auth-play]] - 인증, guest session, `/play -> /plaza` 진입 관련 source
- [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]] - plaza, lobby, room, guest/member 입장 흐름 source
- [[wiki/05-Sources/repos/votedots-public-surface|votedots-public-surface]] - landing, completed canvas, 공개 정적 페이지 source
- [[wiki/05-Sources/repos/votedots-account-analytics|votedots-account-analytics]] - 계정, mypage, 방문 이벤트/집계 source
- [[wiki/05-Sources/repos/votedots-canvas|votedots-canvas]] - canvas 렌더링과 조회 관련 source
- [[wiki/05-Sources/repos/votedots-round-vote|votedots-round-vote]] - round 상태와 vote 흐름 관련 source
- [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]] - summary, history, snapshot 관련 source
- [[wiki/05-Sources/repos/votedots-data-infra|votedots-data-infra]] - data source, session, storage, prod dependency 관련 source
- [[wiki/05-Sources/repos/votedots-schema-entities|votedots-schema-entities]] - migration과 핵심 entity 구조 source
- [[wiki/05-Sources/repos/votedots-summary-persistence|votedots-summary-persistence]] - round/game summary와 snapshot 저장 구조 source
- [[wiki/05-Sources/repos/votedots-quality-ops|votedots-quality-ops]] - test, CI/CD, public page sync, 운영 스크립트 source

## 사용 기준
- repo 전체 그림이 필요하면 `votedots-overview`를 먼저 본다.
- landing, lobby, room, guest/member 계정, 운영/검증 흐름은 새 module source를 먼저 본다.
- 특정 기능 수정 위치를 좁혀야 하면 module source를 먼저 본다.
- 해석과 우선순위 판단은 `02-Architecture`, `03-Status`, `04-Records`에서 한다.
