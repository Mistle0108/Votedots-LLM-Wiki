---
title: Wiki Usage Guide
type: wiki-usage-guide
status: active
updated: 2026-04-23
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
- 이 문서는 사람용 사용 가이드다.
- 연결된 wiki 저장소 문서 해석과 요청 해석 규칙의 기준 진실은 프로젝트 저장소의 `AGENTS.md`다.
- 이 문서는 사용자가 바로 복사해 쓸 수 있는 요청 예시를 제공하는 문서다.

## 세션에서 바로 쓰는 요청 예시
- `wiki 읽고 현재 상태와 다음 작업 정리해줘.`
- `wiki에서 이 내용 확인해봐: history panel`
- `wiki 기준으로 round summary 관련 문서 찾아줘.`
- `wiki 기준으로 이 기능이 왜 이렇게 설계됐는지 설명해줘.`
- `wiki에서 지금 작업과 관련 있는 근거 문서만 모아줘.`
- `wiki 저장소 최신이야?`
- `브랜치 최신 여부 말고, 최근 프로젝트 변경사항이 연결된 wiki 저장소 문서에 실제로 반영됐는지 확인해줘.`
- `지금 완료된 작업 wiki에 등록해줘.`
- `이 PR 끝났으니 wiki 반영 범위 정리해줘.`
- `wiki 규칙 변경 이슈 초안 만들어줘.`
- 사용자는 문서 경로나 문서명을 정확히 몰라도 된다. 주제, 완료된 작업, PR, commit 중 아는 기준만 짧게 말하면 된다.

## 자주 헷갈리는 요청과 추천 문장
- `wiki 저장소 최신이야?`
  - 보통 연결된 wiki 저장소의 원격 기준 최신 여부를 묻는 말로 해석된다.
- `프로젝트 최신 변경이 wiki에 반영됐는지 확인해줘`
  - 의도는 맞지만, 브랜치 최신 여부와 문서 반영 여부가 같이 섞여 들릴 수 있다.
- 문서 반영 여부를 정확히 보고 싶으면 아래처럼 요청하는 편이 안전하다.

```text
브랜치 최신 여부 말고, 최근 프로젝트 변경사항이 연결된 wiki 저장소 문서에 실제로 반영됐는지 확인해줘.
main 기준 최근 변경과 wiki 문서를 대조해서, 반영된 것 / 누락된 것 / 업데이트 필요한 문서를 정리해줘.
```

```text
최근 커밋 10개 기준으로 연결된 wiki 저장소 문서 반영 여부를 검토해줘.
코드와 wiki 문서를 대조해서 누락 항목까지 정리해줘.
```

```text
연결된 wiki 저장소 문서가 최근 기능 수정사항을 따라가고 있는지 확인해줘.
브랜치 최신 여부 말고 문서 내용 기준으로 보고, 업데이트 필요한 문서를 같이 알려줘.
```

- 핵심 표현은 아래 네 가지다.
  - `브랜치 최신 여부 말고`
  - `문서 내용 기준으로`
  - `코드와 wiki를 대조해서`
  - `누락 항목까지`

## 짧은 등록 명령이 의미하는 것
- `지금 완료된 작업 wiki에 등록해줘.`라고 요청하면, LLM은 문서 경로나 반영 절차를 다시 하나씩 묻기보다 현재 프로젝트 세션의 최신 완료 작업을 기준으로 wiki 반영을 시작한다.
- 내부적으로는 보통 아래 순서로 이어진다.
  1. 기준 프로젝트 PR/merge commit 또는 현재 완료 작업 범위 확인
  2. wiki 최신 상태와 기준 `branch + commit` 확인
  3. `05-Sources`, `03-Status`, 필요 시 `04-Records`, `log.md`, `index.md` 반영 필요 여부 정리
  4. 필요한 wiki 브랜치 이름과 PR 초안 제안
- 기준이 모호하면 그때만 최소 질문으로 기준 PR/commit 또는 반영 범위를 확인한다.

## 프로젝트 세션에서 사용하는 기준
- 기본 작업 컨텍스트는 프로젝트 저장소 세션이다.
- 프로젝트 세션에서는 로컬 wiki를 참조해서 현재 상태와 다음 작업을 확인하고, 실제 구현/검증은 프로젝트 저장소에서 진행한다.
- wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 wiki 저장소에서만 진행한다.
- 연결된 wiki 저장소 문서 해석과 요청 해석 규칙은 프로젝트 저장소의 `AGENTS.md`를 기준 진실로 본다.
- 이 문서의 요청 예시는 사람이 의도를 더 정확하게 전달하기 위한 참고 문장이다.
- 프로젝트 세션에서 local wiki 저장소 경로를 확인할 때는 먼저 프로젝트 저장소의 `./.local/wiki-repo.yml`을 사용한다.
- 현재 shell이 WSL이면 `wiki_repo_paths.wsl`, Windows shell이면 `wiki_repo_paths.windows`를 본다.
- 현재 shell 슬롯 값은 프로젝트 세션의 shell에서 실제로 접근 가능한 wiki 경로여야 한다. 프로젝트 `execution_path`가 WSL이면 wiki 경로도 WSL에서 보이는 경로를 쓴다.
- 현재 shell 슬롯 값이 없거나 접근할 수 없으면 LLM은 경로를 한 번만 확인하고 같은 파일의 현재 shell 슬롯에 저장한 뒤, 이후 기본값으로 재사용한다.
- 별도 설명이 없으면 `wiki`는 현재 프로젝트 저장소 내부의 폴더나 브랜치가 아니라 연결된 외부 wiki 저장소 문서를 뜻한다.
- wiki를 근거로 사용자 명령을 수행하기 전에는 먼저 `git fetch origin main`으로 최신 상태를 확인하고 기준 `origin/main@<hash>`를 확정한다.
- 작업이 길어지거나 새로운 요청으로 넘어갈 때도 `git fetch origin main`으로 기준 ref를 다시 확인한다.
- 사용자가 `wiki를 어떻게 사용해?`라고 물으면, LLM은 문서 링크보다 위와 같은 세션용 요청 예시를 먼저 안내해야 한다.
- 사용자는 문서 이름을 모르더라도 `wiki에서 이 내용 확인해봐`, `지금 완료된 작업 wiki에 등록해줘.`처럼 자연어로 요청하면 된다.

## 프로젝트 세션 초기 세팅
- 프로젝트 세션에서 local wiki 저장소 참조를 기본 환경으로 쓰려면 먼저 [[wiki/Home/Project-Session-Setup|Project Session Setup]]를 따라 초기 세팅을 맞춘다.
- 핵심은 프로젝트 저장소의 `./.local/wiki-repo.yml`에 현재 shell 기준 wiki 경로를 저장해 두는 것이다.
- `wiki_repo_paths.<slot>` 값이 없거나 현재 세션에서 접근할 수 없으면 LLM은 자동 추정하지 않고 경로를 한 번만 확인한 뒤 같은 파일의 현재 shell 슬롯에 저장해야 한다.
- `raw/repos/{repo}.local.md`는 `execution_path` 같은 보조 로컬 메타데이터만 관리한다.

## wiki 동기화 확인 기준
- 기본 확인 순서는 `git fetch origin main` -> `git rev-parse origin/main` 이다.
- 두 명령이 성공하면 `origin/main@<hash>`를 기준 commit으로 사용한다.
- `git fetch` 실패 또는 `origin/main` 해시 확인 실패면 최신이라고 단정하지 않고 그 제한과 마지막으로 확인 가능한 기준 commit을 먼저 말한다.
- 커밋된 문서는 원칙적으로 `git show origin/main:<path>` 또는 확정된 `git show <ref>:<path>` 기준으로 읽는다.
- 자동 `pull`, `merge`, `rebase`, 강제 reset은 하지 않는다.

## 최신 확인이 끝났을 때 기대 응답

```text
git fetch origin main 기준으로 최신 상태를 확인했고,
이번 작업 기준은 origin/main@<commit>입니다.
이 기준으로 계속 진행합니다.
```

```text
git fetch origin main이 실패해서 현재 origin/main을 최신 기준이라고 단정할 수 없습니다.
실패 사유와 마지막으로 확인 가능한 기준 상태를 먼저 공유합니다.
```

## 문서 원문 확인 기준
- 커밋된 한글 wiki 문서 원문은 원칙적으로 `git show <ref>:<path>` 기준으로 확인한다.
- 한글 문서를 확인할 때는 PowerShell 기본 출력 인코딩에 기대지 말고, 처음부터 안 깨지는 경로로 읽어 달라고 요청한다.
- 미커밋 변경, 신규 파일, 워킹트리 상태가 필요할 때만 `git diff`, `git status`, 파일 시스템 읽기를 fallback으로 사용한다.
- fallback 파일 읽기가 필요하면 `Get-Content -Encoding utf8`처럼 UTF-8을 명시한 방식으로 읽어 달라고 요청한다.
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
- 텍스트 파일 줄바꿈 기준은 `.gitattributes`를 따르고, 특별한 예외가 없으면 `LF`로 맞춰 달라고 요청하면 된다.

## 이슈 / PR 작성 언어
- LLM이 새로 작성하는 GitHub `issue` 제목/본문, `PR` 제목/본문, 변경 요약은 기본적으로 한글로 작성한다.
- 영어나 다른 언어가 필요하면 사용자가 별도로 요청한다.

## 프로젝트 이슈와 wiki 이슈 구분
- 프로젝트 기능, 버그, 리팩터링 이슈는 대상 코드 repo의 GitHub issue template을 기준으로 요청한다.
- wiki 규칙, 운영 절차, 문서 구조 변경은 wiki 저장소 이슈로 분리해서 요청한다.
- wiki 변경 이슈는 `.github/ISSUE_TEMPLATE/wiki-change-template.md` 기준으로 `배경 -> 목적 -> 작업 범위 -> 확인 기준 -> 비고` 순서로 정리해 달라고 요청하면 된다.
- wiki 규칙/가이드/운영 문서 변경 이슈 제목은 기본적으로 `docs: <주제>` 형식을 사용한다고 함께 요청하면 된다.
- 이슈 생성 요청만으로 브랜치까지 자동 생성하지 않게 하려면 그 조건도 함께 적는다.

## wiki 규칙 변경 요청 예시
```text
wiki 저장소 이슈로 규칙 변경 이슈 초안 만들어줘.
template은 `.github/ISSUE_TEMPLATE/wiki-change-template.md` 기준으로 쓰고,
제목은 `docs: <주제>` 형식으로 잡고,
배경 / 목적 / 작업 범위 / 확인 기준 / 비고 순서로 정리해줘.
작업 브랜치는 아직 만들지 마.
```

```text
wiki 규칙 변경안 반영해줘.
`AGENTS.md`, 사용자 문서, wiki 이슈 template 영향까지 같이 검토하고,
사용자 요청 방식이 바뀌면 `Wiki-Usage-Guide.md`에 예시 요청도 최소 1개 추가해줘.
PR 비고에는 사용자 문서 동기화 여부와 template 변경 여부도 정리해줘.
이 이슈를 완전히 해결하면 `Closes #<번호>`, 일부만 연결되면 `Refs #<번호>`도 넣어줘.
```

## PR 제목 / 본문 초안 기준
- 같은 저장소 이슈를 완전히 해결하면 `비고`에 `Closes #<번호>`를 넣어 달라고 요청한다.
- 관련만 있거나 일부만 반영이면 `Closes` 대신 `Refs #<번호>`를 넣어 달라고 요청한다.
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
프로젝트 세션에서 `./.local/wiki-repo.yml`의 현재 shell 슬롯으로 local wiki repo 경로를 먼저 확인하고,
git fetch origin main 기준으로 wiki 최신 상태와 기준 commit을 먼저 확인해줘.
그 기준 commit으로 현재 상태와 다음 작업을 정리해줘.
원격 확인이 안 되면 그 제한과 마지막으로 확인 가능한 기준 commit을 먼저 말해줘.
```

- 특정 영역만 확인하고 싶으면 범위를 같이 적는다.

```text
프로젝트 세션에서 project-local wiki 설정 기준 local wiki 저장소를 먼저 확인하고,
wiki 최신 상태를 확인한 뒤,
history panel 관련 현재 상태, 남은 작업, 참고할 근거 문서를 정리해줘.
```

- 기대 결과는 아래 4가지다.
  - 현재 완료된 작업
  - 현재 gap이 남아 있는 작업
  - 다음 우선 작업
  - 각 항목의 근거 문서

## LLM에게 작업 완료 후 반영을 요청하는 방법
- 가장 단순한 요청은 아래 한 줄이면 된다.

```text
지금 완료된 작업 wiki에 등록해줘.
```

- 이 요청을 받으면 LLM은 보통 아래 순서로 이어서 정리한다.
  - 현재 프로젝트 세션에서 기준 프로젝트 PR/merge commit 또는 완료 작업 범위 확인
  - wiki 최신 상태와 기준 `branch + commit` 확인
  - `05-Sources`, `03-Status`, 필요 시 `04-Records`, `log.md`, `index.md` 반영 필요 여부 정리
  - wiki 저장소 브랜치 이름과 PR 초안 제안
- 기준을 더 강하게 고정하고 싶으면 아래처럼 추가 정보를 준다.

- 기능 PR이 merge된 뒤에는 아래처럼 요청한다.

```text
프로젝트 PR이 끝났으니 프로젝트 세션에서 git fetch origin main 기준으로
wiki 최신 상태와 기준 commit을 먼저 확인해줘.
그다음 프로젝트 main 브랜치 최신 merge commit 기준으로 wiki 반영이 필요한 내용을 정리해줘.
필요하면 wiki 저장소에서 만들 wiki 브랜치 이름도 제안하고,
PR 제목은 `pr: <번호> <주제>` 형식으로, 본문은 `기준 작업 / 변경 요약 / 반영 문서 / 비고` 순서로 한글 초안 정리해줘.
커밋/PR/merge는 내 동의를 받아 진행해줘.
```

- 특정 merge commit을 기준으로 고정하고 싶으면 commit hash를 같이 준다.

```text
프로젝트 main@<commit> 기준으로 wiki를 갱신해줘.
wiki 쪽은 git fetch origin main 기준으로 최신 상태와 기준 commit을 먼저 확인하고,
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
  - `git fetch origin main` 기준 최신 ref 확인
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
1. 프로젝트 세션에서 사용자의 새 요청을 처리하기 전에 LLM이 `git fetch origin main`으로 wiki 최신 상태와 기준 `origin/main@<hash>`를 확인한다.
2. 사용자는 `wiki 읽고 현재 상태와 다음 작업 정리해줘.`처럼 짧게 요청할 수 있다.
3. 필요한 경우 `System Reference`, `Data Flow`, `Records`, `Sources`까지 확장해서 읽게 한다.
4. 프로젝트 저장소에서 기능 작업과 PR merge가 완료되면, 같은 프로젝트 세션에서 `지금 완료된 작업 wiki에 등록해줘.`처럼 간단하게 wiki 반영을 요청할 수 있다.
5. LLM은 `git fetch origin main`으로 기준 ref를 다시 확인한 뒤, 필요하면 wiki 저장소에서 `docs/<topic-slug>` 또는 `pr/<project-pr-number>-<topic-slug>` 브랜치를 만들도록 반영 계획을 제안한다.
6. LLM이 변경 내용을 요약하면 사람이 검토하고, 동의가 있을 때만 wiki 커밋, PR, main 머지를 순서대로 진행한다.
