---
title: Home
type: home
status: active
updated: 2026-04-23
tags:
  - wiki
  - home
---

# Home

## 목적
이 wiki는 Votedots 프로젝트의 공식 문서, 산출물, 개발 기록 저장소다.  
작업 현황은 별도 보드가 아니라 공식 문서를 읽었을 때 자연스럽게 파악되도록 유지한다.

## 사용 전 확인
- wiki를 기준으로 현재 상태, 다음 작업, 반영 범위를 말하기 전에는 먼저 `git fetch origin main`으로 최신 상태를 확인하고 `origin/main@<hash>`를 기준으로 잡는다.
- 프로젝트 작업은 프로젝트 저장소 세션에서 진행하고, wiki는 같은 세션에서 로컬 참조 문서로 읽는다.
- 프로젝트 세션에서 wiki 경로 bootstrap과 `wiki` 요청 해석 기준은 프로젝트 저장소의 `AGENTS.md`를 따른다.
- 원격 최신 확인이 불가능하면 최신이라고 단정하지 말고, 실제 사용 기준 `branch + commit`을 먼저 밝힌다.

## 프로젝트 세션 초기 세팅
- 프로젝트 세션에서 local wiki 저장소를 기본 참조로 쓰려면 먼저 [Project Session Setup](wiki/Home/Project-Session-Setup.md)를 따라 초기 세팅을 맞춘다.
- 핵심은 프로젝트 저장소의 `./.local/wiki-repo.yml`에 현재 shell 기준 wiki 경로를 저장해 두는 것이다.
- 현재 shell이 WSL이면 `wiki_repo_paths.wsl`, Windows shell이면 `wiki_repo_paths.windows`를 사용한다.
- 경로가 없거나 접근이 안 되면 한 번만 확인하고 같은 파일의 현재 shell 슬롯에 저장한 뒤 이후 기본값으로 재사용한다.
- 프로젝트 `execution_path`가 WSL이면 wiki 경로도 WSL에서 보이는 경로를 쓴다.

## 빠른 사용 예시
- `wiki 읽고 현재 상태와 다음 작업 정리해줘.`
- `wiki에서 이 내용 확인해봐: history panel`
- `wiki 기준으로 round summary 관련 문서 찾아줘.`
- `wiki 기준으로 이 기능이 왜 이렇게 설계됐는지 설명해줘.`
- `지금 완료된 작업 wiki에 등록해줘.`
- `wiki 규칙 변경 이슈 초안 만들어줘.`
- 사용자는 문서 경로를 몰라도 주제나 완료된 작업만 짧게 말하면 된다.

## 현재 기준
| 항목 | 값 |
| --- | --- |
| 코드 기준 커밋 | `Votedots main@fecd28db8d164c4cbfe2dab72e20df395380321b` |
| wiki 사용 원칙 | `git fetch origin main` 후 `origin/main@<hash>` 기준으로 읽기 |
| 프로젝트 세션 초기 세팅 | [[wiki/Home/Project-Session-Setup|Project Session Setup]] |
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
1. `git fetch origin main`으로 최신 상태를 확인하고 기준 `origin/main@<hash>`를 확정한다.
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
- 사용자는 `지금 완료된 작업 wiki에 등록해줘.`처럼 짧게 요청해도 된다.
- LLM은 이를 현재 프로젝트 세션의 완료 작업 기준으로 wiki 반영 범위를 정리해 달라는 요청으로 해석한다.
- 먼저 기준 프로젝트 PR/merge commit 또는 완료 작업 범위를 확인하고, `05-Sources`, `03-Status`, 필요 시 `04-Records`, `log.md`, `index.md` 반영 여부를 정리한다.
- 프로젝트 브랜치 PR이 완료되고 사용자가 wiki 등록을 요청하면, 같은 프로젝트 세션에서 반영 범위를 먼저 정리한다.
- 반영 범위 정리는 프로젝트 세션에서 하더라도, 실제 wiki 반영 브랜치 생성과 wiki git 작업은 wiki 저장소에서 진행한다.
- wiki 반영 직전에는 `git fetch origin main`으로 기준 `origin/main@<hash>`를 다시 확인한다.
- wiki 반영 브랜치는 규칙/가이드 수정이면 `docs/<topic-slug>`를 사용하고, 특정 프로젝트 PR에 대응하는 반영이면 `pr/<project-pr-number>-<topic-slug>` 형식을 사용한다.
- 새로 작성하는 GitHub `issue`/`PR` 제목, 본문, 요약은 기본적으로 한글로 작성한다.
- 동기화 확인 명령, PR 반영 체크리스트, `<topic-slug>` 규칙의 상세 내용은 `wiki/AGENTS.md`와 `Wiki-Operating-Rules.md`를 따른다.
- 문서 수정 후에는 사용자 동의를 받아 커밋, PR, main 머지 순으로 진행한다.

## 참고 문서
- 프로젝트 세션 초기 세팅: [[wiki/Home/Project-Session-Setup|Project Session Setup]]
- 팀 공유용 운영 설명서: [[wiki/Home/Wiki-Operating-Rules|Wiki Operating Rules]]
- 실제 사용 가이드: [[wiki/Home/Wiki-Usage-Guide|Wiki Usage Guide]]
- 프로젝트 세션 요청 해석 기준: 프로젝트 저장소의 `/AGENTS.md`
- wiki 저장소 루트 진입 규칙: `/AGENTS.md`
- wiki 내부 작업 규칙: `wiki/AGENTS.md`

## baseline 상태
- 현재 baseline은 `Votedots main@fecd28db8d164c4cbfe2dab72e20df395380321b` 기준으로 near-ready 상태다.
- `Project / Architecture / Status / Records / Sources` 핵심 문서 축은 연결되어 있다.
- history timeline, 중앙 viewport, summary modal, interaction polish 반영까지 문서 기준선에 포함돼 있다.
- `Next Work`에 남아 있는 항목은 문서 공백보다 프로젝트 구현 / 정렬 과제에 가깝다.
