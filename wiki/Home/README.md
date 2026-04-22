---
title: Home
type: home
status: active
updated: 2026-04-22
tags:
  - wiki
  - home
---

# Home

## 목적
이 wiki는 Votedots 프로젝트의 공식 문서, 산출물, 개발 기록 저장소다.  
작업 현황은 별도 보드가 아니라 공식 문서를 읽었을 때 자연스럽게 파악되도록 유지한다.

## 사용 전 확인
- wiki를 기준으로 현재 상태, 다음 작업, 반영 범위를 말하기 전에는 먼저 wiki 로컬 `main`과 `origin/main`이 같은지 확인한다.
- 프로젝트 작업은 프로젝트 저장소 세션에서 진행하고, wiki는 같은 세션에서 로컬 참조 문서로 읽는다.
- 원격 최신 확인이 불가능하거나 로컬/원격이 다르면 최신이라고 단정하지 말고, 실제 사용 기준 `branch + commit`을 먼저 밝힌다.

## 현재 기준
| 항목 | 값 |
| --- | --- |
| 코드 기준 커밋 | `Votedots main@31d22b3535627b3a0a56ea1cf9e41411475f72fd` |
| wiki 사용 원칙 | 로컬 `main`과 `origin/main` 일치 확인 후 읽기 |
| 프로젝트 정의 문서 | [[wiki/01-Project/README|01-Project]] |
| 구조 문서 | [[wiki/02-Architecture/System-Reference|System Reference]] |
| 흐름 문서 | [[wiki/02-Architecture/Data-Flow|Data Flow]] |
| 운영 아키텍처 문서 | [[wiki/02-Architecture/Operations|Operations]] |
| 현재 상태 문서 | [[wiki/03-Status/Current-State|Current State]] |
| 다음 작업 문서 | [[wiki/03-Status/Next-Work|Next Work]] |
| 기록 문서 | [[wiki/04-Records/README|04-Records]] |
| 근거 source 문서 | [[wiki/05-Sources/README|05-Sources]] |
| 운영 규칙 문서 | [[wiki/Home/Wiki-Operating-Rules|Wiki Operating Rules]] |
| 사용 가이드 문서 | [[wiki/Home/Wiki-Usage-Guide|Wiki Usage Guide]] |

## 읽는 순서
1. wiki 로컬 `main`과 `origin/main` 최신 상태를 확인한다.
2. [[wiki/index|index]]
3. [[wiki/Home/README|Home]]
4. [[wiki/03-Status/Current-State|Current State]]
5. [[wiki/03-Status/Next-Work|Next Work]]
6. [[wiki/02-Architecture/System-Reference|System Reference]]
7. [[wiki/02-Architecture/Data-Flow|Data Flow]]
8. [[wiki/04-Records/README|04-Records]]
9. [[wiki/05-Sources/README|05-Sources]]

## 질문별 진입점
| 확인 목적 | 먼저 볼 문서 | 비고 |
| --- | --- | --- |
| 프로젝트가 무엇인가 | [[wiki/01-Project/README|01-Project]] | 범위와 핵심 흐름 확인 |
| 지금 어디까지 됐는가 | [[wiki/03-Status/Current-State|Current State]] | 완료 / 부분 완료 / gap 확인 |
| 다음에 무엇을 해야 하는가 | [[wiki/03-Status/Next-Work|Next Work]] | 우선순위와 이유 확인 |
| 어느 코드를 봐야 하는가 | [[wiki/02-Architecture/System-Reference|System Reference]] | 책임 위치와 핵심 모듈 확인 |
| 화면과 상태가 어떻게 이어지는가 | [[wiki/02-Architecture/Data-Flow|Data Flow]] | auth/play/round/vote/history 흐름 확인 |
| 왜 이렇게 됐는가 | [[wiki/04-Records/README|04-Records]] | 작업, 문제, 결정 이력 확인 |
| 근거가 무엇인가 | [[wiki/05-Sources/README|05-Sources]] | repo / issue / PR 사실 확인 |
| 운영 기준이 무엇인가 | [[wiki/Home/Wiki-Operating-Rules|Wiki Operating Rules]] | 팀 운영 기준 확인 |

## wiki 반영 시작점
- 프로젝트 브랜치 PR이 완료되고 사용자가 wiki 등록을 요청하면, 같은 프로젝트 세션에서 반영 범위를 먼저 정리한다.
- 반영 범위 정리는 프로젝트 세션에서 하더라도, 실제 wiki 반영 브랜치 생성과 wiki git 작업은 wiki 저장소에서 진행한다.
- wiki 반영 직전에는 wiki 로컬 `main`과 `origin/main`이 같은지 다시 확인한다.
- wiki 반영 브랜치는 규칙/가이드 수정이면 `docs/<topic-slug>`를 사용하고, 특정 프로젝트 PR에 대응하는 반영이면 `pr/<project-pr-number>-<topic-slug>` 형식을 사용한다.
- 새로 작성하는 GitHub `issue`/`PR` 제목, 본문, 요약은 기본적으로 한글로 작성한다.
- 동기화 확인 명령, PR 반영 체크리스트, `<topic-slug>` 규칙의 상세 내용은 `wiki/AGENTS.md`와 `Wiki-Operating-Rules.md`를 따른다.
- 문서 수정 후에는 사용자 동의를 받아 커밋, PR, main 머지 순으로 진행한다.

## 참고 문서
- 팀 공유용 운영 설명서: [[wiki/Home/Wiki-Operating-Rules|Wiki Operating Rules]]
- 실제 사용 가이드: [[wiki/Home/Wiki-Usage-Guide|Wiki Usage Guide]]
- LLM 전역 규칙: `/AGENTS.md`
- wiki 내부 작업 규칙: `wiki/AGENTS.md`

## baseline 상태
- 현재 baseline은 `Votedots main@31d22b3535627b3a0a56ea1cf9e41411475f72fd` 기준으로 near-ready 상태다.
- `Project / Architecture / Status / Records / Sources` 핵심 문서 축은 연결되어 있다.
- `Next Work`에 남아 있는 항목은 문서 공백보다 프로젝트 구현 / 정렬 과제에 가깝다.
