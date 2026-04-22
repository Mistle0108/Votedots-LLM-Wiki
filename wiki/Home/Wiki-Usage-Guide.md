---
title: Wiki Usage Guide
type: wiki-usage-guide
status: active
updated: 2026-04-22
tags:
  - wiki
  - home
  - usage-guide
---

# Wiki Usage Guide

## 목적
- 이 문서는 팀원이 Votedots wiki를 실제로 어떻게 사용해야 하는지 빠르게 안내한다.
- 목적은 아래 3가지를 쉽게 수행하게 하는 것이다.
  - 작업 시작 전에 현재 상태와 다음 작업을 확인하기
  - 작업 완료 후 wiki에 반영이 필요한 내용을 판단하기
  - LLM에게 어떤 방식으로 요청해야 하는지 바로 알기
- 이 문서는 사람용 사용 가이드다. LLM 실행 규칙의 원본은 `AGENTS.md`, `wiki/AGENTS.md`다.

## 프로젝트 세션에서 사용하는 기준
- 기본 작업 컨텍스트는 프로젝트 저장소 세션이다.
- 프로젝트 세션에서는 로컬 wiki를 참조해서 현재 상태와 다음 작업을 확인하고, 실제 구현/검증은 프로젝트 저장소에서 진행한다.
- wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 wiki 저장소에서만 진행한다.
- wiki를 근거로 사용자 명령을 수행하기 전에는 먼저 wiki 로컬 `main`과 `origin/main`이 같은지 확인한다.
- 작업이 길어지거나 새로운 요청으로 넘어갈 때도 wiki 로컬/원격 일치 여부를 다시 확인한다.

## wiki 동기화 확인 기준
- 기본 확인 순서는 `git fetch origin main` -> `git rev-parse main` -> `git rev-parse origin/main` 이다.
- 두 해시가 같으면 `wiki local main == origin/main`으로 보고, `main@<hash>`를 기준 commit으로 사용한다.
- `git fetch` 실패, `main` 부재, 해시 불일치면 최신이라고 단정하지 않고 그 제한과 현재 기준 commit을 먼저 말한다.
- 자동 `pull`, `merge`, `rebase`는 하지 않고 사용자와 기준 상태를 먼저 맞춘다.
- 해시가 다르면 먼저 불일치 사실을 알리고, 가능하면 로컬 `main`을 `origin/main`에 `fast-forward`로 맞춘 뒤 새 기준 commit으로 계속 진행한다.
- `main` 전환이 안 되거나 `fast-forward`가 실패하면 자동 `merge`, `rebase`, 강제 reset 없이 실패 사유를 먼저 설명한다.

## sync 불일치가 났을 때 기대 응답

```text
wiki 로컬 main과 origin/main이 다릅니다.
먼저 로컬 main을 origin/main에 fast-forward로 맞춘 뒤, 새 기준 commit으로 계속 진행하겠습니다.
```

```text
wiki local main을 origin/main@<commit>으로 fast-forward 했습니다.
이제 main@<commit> 기준으로 계속 진행합니다.
```

```text
wiki 로컬 main과 origin/main이 다르지만, 현재 상태에서는 main 전환 또는 fast-forward가 불가능합니다.
자동 merge/rebase는 하지 않고, 실패 사유와 현재 기준 상태를 먼저 공유합니다.
```

## 문서 원문 확인 기준
- 커밋된 한글 wiki 문서 원문은 원칙적으로 `git show <ref>:<path>` 기준으로 확인한다.
- 미커밋 변경, 신규 파일, 워킹트리 상태가 필요할 때만 `git diff`, `git status`, 파일 시스템 읽기를 fallback으로 사용한다.
- 같은 문서를 이미 commit 기준으로 읽었다면, 같은 턴에서 PowerShell 파일 읽기로 다시 중복 확인하지 않는 것을 기본으로 본다.

## `git show` 사용 기준 표

| 확인하려는 것 | 먼저 쓸 방식 | fallback | 메모 |
| --- | --- | --- | --- |
| 커밋된 한글 wiki 문서 원문 | `git show <ref>:<path>` | 없음 | 기준 commit을 먼저 정한다. |
| 같은 커밋 문서의 특정 부분만 다시 확인 | `git show <ref>:<path>` 후 필요한 부분만 확인 | 없음 | 같은 턴에서 PowerShell 재확인을 기본으로 하지 않는다. |
| 미커밋 변경 | `git diff -- <path>` | 파일 시스템 읽기 | 아직 baseline이 아니다. |
| 신규 파일 | 파일 시스템 읽기 | 없음 | Git 객체에 아직 없어서 `git show`로 못 읽는다. |
| 워킹트리 상태 | `git status` | 파일 시스템 읽기 | 커밋 기준 내용과 구분해서 본다. |

## wiki 브랜치 이름 기준
- 규칙/가이드/운영 문서 수정은 `docs/<topic-slug>`를 사용한다.
- 특정 프로젝트 PR 반영은 `pr/<project-pr-number>-<topic-slug>`를 사용한다.
- `<topic-slug>`는 소문자 영어, 숫자, 하이픈만 사용하고 kebab-case 2~6단어 정도로 유지한다.
- `docs`, `pr`, `branch`, `update`, `misc`, 날짜, PR 번호처럼 prefix에 이미 있는 정보는 slug에 반복하지 않는다.

## wiki 작업 브랜치 생성 기준
- 새 작업 브랜치가 필요하면 LLM은 먼저 `git fetch origin main`으로 원격 최신 상태를 확인한다.
- 브랜치는 원칙적으로 로컬 `main`이 아니라 `origin/main`을 직접 기준으로 만든다.
- 원격 확인이 실패하면 최신이라고 단정하지 않고 실패 사유를 먼저 설명해야 한다.
- 브랜치를 만든 뒤에는 이번 작업의 기준 `branch + commit`을 함께 알려 달라고 요청하면 된다.

## wiki 문서 수정 방식
- wiki 문서 정합성 검증이 필요한 변경은 초안 메모만 따로 두기보다 작업 브랜치에서 실제 문서를 바로 수정해 달라고 요청하는 편이 낫다.
- 여러 문서가 함께 바뀌는 규칙 변경이면 영향 문서도 같은 브랜치에서 같이 수정해 달라고 요청한다.
- 검증 기준은 워킹트리 자체가 아니라 기준 `branch + commit`, diff, 반영 문서 목록으로 설명해 달라고 요청하면 된다.

## 이슈 / PR 작성 언어
- LLM이 새로 작성하는 GitHub `issue` 제목/본문, `PR` 제목/본문, 변경 요약은 기본적으로 한글로 작성한다.
- 영어나 다른 언어가 필요하면 사용자가 별도로 요청한다.

## 프로젝트 이슈와 wiki 이슈 구분
- 프로젝트 기능, 버그, 리팩터링 이슈는 대상 코드 repo의 GitHub issue template을 기준으로 요청한다.
- wiki 규칙, 운영 절차, 문서 구조 변경은 wiki 저장소 이슈로 분리해서 요청한다.
- wiki 변경 이슈는 `.github/ISSUE_TEMPLATE/wiki-change-template.md` 기준으로 `배경 -> 목적 -> 작업 범위 -> 확인 기준 -> 비고` 순서로 정리해 달라고 요청하면 된다.
- 이슈 생성 요청만으로 브랜치까지 자동 생성하지 않게 하려면 그 조건도 함께 적는다.

## wiki 규칙 변경 요청 예시
```text
wiki 저장소 이슈로 규칙 변경 이슈 초안 만들어줘.
template은 `.github/ISSUE_TEMPLATE/wiki-change-template.md` 기준으로 쓰고,
배경 / 목적 / 작업 범위 / 확인 기준 / 비고 순서로 정리해줘.
작업 브랜치는 아직 만들지 마.
```

```text
wiki 규칙 변경안 반영해줘.
`AGENTS.md`, 사용자 문서, wiki 이슈 template 영향까지 같이 검토하고,
사용자 요청 방식이 바뀌면 `Wiki-Usage-Guide.md`에 예시 요청도 최소 1개 추가해줘.
PR 비고에는 사용자 문서 동기화 여부와 template 변경 여부도 정리해줘.
```

## PR 제목 / 본문 초안 기준
- wiki 규칙/가이드/운영 문서 수정용 PR 제목 초안은 `docs: <주제>` 형식을 사용한다.
- 프로젝트 PR 반영용 PR 제목 초안은 `pr: <project-pr-number> <주제>` 형식을 사용한다.
- `docs` 본문 초안은 `변경 요약 -> 반영 문서 -> 비고` 순서를 사용한다.
- `pr` 본문 초안은 `기준 작업 -> 변경 요약 -> 반영 문서 -> 비고` 순서를 사용한다.

## 이 wiki에서 먼저 보면 되는 문서
- [[wiki/Home/README|Home]]
  - wiki 진입점, 기준 커밋, 읽는 순서를 확인한다.
- [[wiki/03-Status/Current-State|Current State]]
  - 지금 기준 커밋에서 이미 구현된 상태를 확인한다.
- [[wiki/03-Status/Next-Work|Next Work]]
  - 다음 우선 작업과 남은 gap을 확인한다.
- [[wiki/02-Architecture/System-Reference|System Reference]]
  - 어느 코드 영역을 봐야 하는지 확인한다.
- [[wiki/04-Records/README|04-Records]]
  - 왜 이런 구조와 결정이 되었는지 확인한다.
- [[wiki/05-Sources/README|05-Sources]]
  - repo, issue, PR 근거 문서를 확인한다.

## 언제 wiki를 확인해야 하는가
- 사용자의 새 명령을 수행하기 전
- 새 작업을 시작하기 전
- 다른 사람이 진행하던 작업을 이어받기 전
- 현재 우선순위와 남은 작업을 다시 확인해야 할 때
- 특정 기능이 왜 그렇게 구현되었는지 배경이 필요할 때
- 관련 코드 위치와 참고 근거 문서를 빠르게 찾아야 할 때

## 언제 wiki를 갱신해야 하는가
- 프로젝트 repo의 기능 PR이 기준 브랜치에 merge된 뒤
- 기준 커밋 기준 현재 상태가 바뀌었을 때
- 다음 우선 작업이나 선행 조건이 바뀌었을 때
- 중요한 문제, 결정, 이력이 새로 생겼을 때
- 새 source 문서나 기록 문서를 추가해야 할 만큼 재사용 가치가 생겼을 때

## LLM에게 현재 상태를 물어보는 방법
- 작업 시작 전에는 아래처럼 요청한다.

```text
프로젝트 세션에서 로컬 wiki와 origin/main이 같은지 먼저 확인하고,
다르면 먼저 불일치 사실을 알리고 local main을 origin/main에 fast-forward로 맞춘 뒤,
그 기준 commit으로 현재 상태와 다음 작업을 정리해줘.
원격 확인이 안 되거나 로컬/원격이 다르면 그 제한과 기준 commit을 먼저 말해줘.
```

- 특정 영역만 확인하고 싶으면 범위를 같이 적는다.

```text
프로젝트 세션에서 wiki 최신 상태를 먼저 확인하고,
history panel 관련 현재 상태, 남은 작업, 참고할 근거 문서를 정리해줘.
```

- 기대 결과는 아래 4가지다.
  - 현재 완료된 작업
  - 현재 gap이 남아 있는 작업
  - 다음 우선 작업
  - 각 항목의 근거 문서

## LLM에게 작업 완료 후 반영을 요청하는 방법
- 기능 PR이 merge된 뒤에는 아래처럼 요청한다.

```text
프로젝트 PR이 끝났으니 프로젝트 세션에서 wiki 로컬 main과 origin/main이 같은지 먼저 확인해줘.
다르면 먼저 불일치 사실을 알리고 local main을 origin/main에 fast-forward로 맞춘 뒤,
프로젝트 main 브랜치 최신 merge commit 기준으로 wiki 반영이 필요한 내용을 정리해줘.
필요하면 wiki 저장소에서 만들 wiki 브랜치 이름도 제안하고,
PR 제목은 `pr: <번호> <주제>` 형식으로, 본문은 `기준 작업 / 변경 요약 / 반영 문서 / 비고` 순서로 한글 초안 정리해줘.
커밋/PR/merge는 내 동의를 받아 진행해줘.
```

- 특정 merge commit을 기준으로 고정하고 싶으면 commit hash를 같이 준다.

```text
프로젝트 main@<commit> 기준으로 wiki를 갱신해줘.
wiki 로컬 main과 origin/main이 같은지 먼저 확인하고,
필요하면 wiki 저장소에서 만들 `pr/<번호>-<주제>` 형식의 wiki 브랜치 이름을 제안해줘.
Current-State, Next-Work, 필요한 Sources/Records까지 반영하고,
PR 제목은 `pr: <번호> <주제>` 형식으로, 본문은 `기준 작업 / 변경 요약 / 반영 문서 / 비고` 순서로 한글 초안 정리해줘.
```

- wiki 규칙/가이드/운영 문서 자체를 수정한 경우에는 아래처럼 요청한다.

```text
이번 작업은 wiki 운영 규칙 수정이니,
wiki 저장소용 브랜치 이름을 제안하고 `docs: <주제>` 형식의 PR 제목과
`변경 요약 / 반영 문서 / 비고` 순서의 한글 본문 초안을 정리해줘.
```

- 기대 결과는 아래 순서를 따른다.
  - wiki 로컬/원격 최신 상태 확인
  - 기준 branch + commit 확인
  - `Current-State`, `Next-Work`, 관련 `05-Sources`, 필요 시 `04-Records` 확인
  - 필요한 raw/source/status/records 반영
  - 새 문서 추가/삭제/이름 변경이 있으면 `index.md` 반영
  - 의미 있는 변경이면 `log.md` 기록
  - 변경 요약 제시
  - 사용자 승인 후 커밋
  - 사용자 승인 후 PR 요청

## 언제 사용자 문서도 같이 갱신해야 하는가
- `AGENTS.md`, `wiki/AGENTS.md`, wiki 운영 절차, publish 절차, 요청 방식 규칙을 바꿨을 때
- 팀 운영 설명이 바뀌면 `wiki/Home/Wiki-Operating-Rules.md`를 같이 검토한다.
- 사람용 요청 예시나 사용 흐름이 바뀌면 `wiki/Home/Wiki-Usage-Guide.md`를 같이 검토한다.
- `AGENTS.md` 계열과 사용자 문서가 충돌하면 `AGENTS.md` 계열을 기준으로 보고, 같은 브랜치와 같은 PR 범위에서 사용자 문서도 함께 정정한다.
- 요청 방식이나 승인 흐름이 바뀌면 `Wiki-Usage-Guide.md`에 예시 요청을 최소 1개 추가한다.
- 규칙 변경을 요청할 때는 `사용자 문서도 같이 검토하고 필요하면 업데이트해줘`라고 함께 적으면 누락이 줄어든다.

## 작업 흐름 예시
1. 프로젝트 세션에서 사용자의 새 요청을 처리하기 전에 LLM이 wiki 로컬 `main`과 `origin/main`이 같은지 확인한다.
2. LLM에게 wiki를 읽고 현재 상태와 다음 작업을 정리해달라고 요청한다.
3. 필요한 경우 `System Reference`, `Data Flow`, `Records`, `Sources`까지 확장해서 읽게 한다.
4. 프로젝트 저장소에서 기능 작업과 PR merge가 완료되면, 같은 프로젝트 세션에서 merge commit 기준으로 wiki 반영을 요청한다.
5. LLM은 wiki 로컬 `main`과 `origin/main`을 다시 확인한 뒤, 필요하면 wiki 저장소에서 `docs/<topic-slug>` 또는 `pr/<project-pr-number>-<topic-slug>` 브랜치를 만들도록 반영 계획을 제안한다.
6. LLM이 변경 내용을 요약하면 사람이 검토하고, 동의가 있을 때만 wiki 커밋, PR, main 머지를 순서대로 진행한다.
