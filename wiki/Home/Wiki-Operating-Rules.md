---
title: Wiki Operating Rules
type: wiki-operating-rules
status: active
updated: 2026-04-23
tags:
  - wiki
  - home
  - operating-rules
---

# Wiki Operating Rules

## 목적
- 이 문서는 팀이 공유하는 wiki 운영 설명서다.
- 목표는 아래 3가지를 같은 기준으로 다루는 것이다.
  - wiki를 어디서부터 읽을지
  - 어떤 문서를 어디에 써야 할지
  - 기준 커밋 기반으로 어떻게 갱신하고 publish할지
- 추가로 프로젝트 저장소 세션에서 wiki를 어떻게 참조하고 반영 요청까지 이어갈지 명확히 한다.

## 저장소 구조
```text
raw/      # 원본 또는 원본 참조 정보
wiki/     # 공식 문서
Output/   # 세션 결과, 임시 분석, 보고 초안
```

## 문서 역할 분리
- `/README.md`
  - 저장소 첫 화면용 짧은 안내문
- `/AGENTS.md`
  - 저장소 루트 진입 규칙과 전역 행동 규칙
- `/wiki/AGENTS.md`
  - `wiki/` 내부 작업 상세 규칙
- `/wiki/Home/README.md`
  - wiki 진입점
- `/wiki/Home/Wiki-Operating-Rules.md`
  - 팀 공유용 운영 설명서
- 역할 분리 원칙:
  - 루트 `AGENTS.md`는 wiki 저장소 루트 진입 규칙과 전역 기본값을 다룬다.
  - `wiki/AGENTS.md`는 wiki 문서 읽기/쓰기/publish의 상세 절차를 다룬다.
  - 프로젝트 저장소의 `AGENTS.md`는 프로젝트 세션의 wiki 경로 bootstrap과 연결된 wiki 저장소 문서 해석, 요청 해석 규칙의 기준 진실이다.
  - `wiki/Home/Wiki-Usage-Guide.md`는 사람용 요청 예시를 다루며, LLM 실행 규칙의 원본이 아니다.
  - 두 파일은 둘 다 유지하되, 같은 상세 규칙을 중복 복사하지 않는다.

## 전제
- 저장소 구조 자체는 위 형태로 유지한다.
- 이 문서에서 자세히 설명하는 것은 repo 전체 구조가 아니라 `wiki/` 내부 구조와 운영 기준이다.

## wiki 구조
```text
wiki/
  Home/               # 진입점, 읽는 순서, 운영 규칙, 핵심 링크
  01-Project/         # 프로젝트 정의 문서
  02-Architecture/    # 시스템 구조, 데이터 흐름, 운영 아키텍처
  03-Status/          # 현재 상태, 다음 작업
  04-Records/         # 작업 기록, 문제, 결정
  05-Sources/         # repo / issue / PR 사실 요약
  index.md            # 전체 문서 카탈로그
  log.md              # wiki 운영 이력
```

## 문서 역할
- `01-Project`
  - 프로젝트가 무엇인지 설명하는 공식 문서
- `02-Architecture`
  - 시스템이 어떻게 구성되어 있고 흐름이 어떻게 이어지는지 설명하는 문서
- `03-Status/Current-State.md`
  - 지금 기준 커밋에서 이미 사실인 상태를 적는 문서
- `03-Status/Next-Work.md`
  - `Current-State`를 읽은 뒤 다음에 해야 할 작업을 적는 문서
- `04-Records`
  - 작업, 문제, 결정 이력을 축적하는 문서
- `05-Sources`
  - repo / issue / PR의 사실만 적는 근거 문서
- `index.md`
  - 전체 문서 목록과 탐색 구조
- `log.md`
  - wiki가 언제 무엇 때문에 갱신됐는지 남기는 운영 로그
  - git commit 로그 대체물이 아니라, wiki 운영 관점의 의미 있는 변경을 남기는 문서

## 기준 진실
```text
code@commit
> merged PR
> open PR
> issue
> output/session
```

## 기준 커밋 원칙
- wiki는 항상 특정 `branch + commit` 기준으로 작성한다.
- 기준 진실은 항상 `code@commit`이다.
- 미커밋 변경은 baseline에 포함하지 않는다.
- 같은 질문은 같은 `commit` 기준이면 같은 답이 나와야 한다.
- 사용자의 명령을 wiki 기준으로 수행하기 전에는 먼저 `git fetch origin main`으로 원격 최신 상태를 확인한다.
- `git fetch`가 성공하면 `git rev-parse origin/main`으로 `origin/main@<hash>`를 기준 commit으로 확정한다.
- 원격 확인이 불가능하면 최신이라고 단정하지 말고, 제한과 실제 사용 기준 `branch + commit`을 먼저 밝힌다.

## wiki 동기화 확인 절차
1. 기본 명령 순서는 `git fetch origin main` -> `git rev-parse origin/main` 이다.
2. 두 명령이 성공하면 `origin/main@<hash>`를 이번 읽기/쓰기 기준으로 확정한다.
3. 커밋된 문서는 원칙적으로 `git show origin/main:<path>` 또는 확정된 `git show <ref>:<path>` 기준으로 읽는다.
4. `git fetch`가 실패하면 최신이라고 단정하지 않고, 제한과 마지막으로 확인 가능한 기준 `branch + commit`만 먼저 밝힌다.
5. `origin/main` 해시를 읽지 못하면 현재 세션에서 최신 기준 ref를 확정하지 못했다는 사실을 먼저 밝힌다.
6. 긴 작업 중 새 요청 시작 전이나 중요한 판단 직전에는 이 절차를 다시 수행한다.

## 최신 확인 응답 예시
- 성공 예시:

```text
git fetch origin main 기준으로 최신 상태를 확인했고,
이번 작업 기준은 origin/main@<commit>입니다.
이 기준으로 계속 진행합니다.
```

- 실패 예시:

```text
git fetch origin main이 실패해서 현재 origin/main을 최신 기준이라고 단정할 수 없습니다.
실패 사유와 마지막으로 확인 가능한 기준 상태를 먼저 공유합니다.
```

## 작업 브랜치 생성 기준
- 새 작업 브랜치가 필요하면 원칙적으로 `git fetch origin main` 후 `origin/main`을 직접 기준으로 만든다.
- 로컬 `main` 최신화는 읽기/쓰기 기준 확인에는 중요하지만, 브랜치 생성의 필수 선행 조건으로 두지 않는다.
- 원격 확인이 실패하면 `origin/main`을 최신 기준이라고 단정하지 않고 실패 사유를 먼저 공유한다.
- 브랜치를 만든 뒤에는 이번 작업의 기준 `branch + commit`을 함께 남긴다.

## wiki 문서 직접 수정 원칙
- wiki 문서 정합성 검증이 필요한 변경은 작업 브랜치에서 실제 문서를 바로 수정하는 방식을 기본으로 한다.
- 메모나 임시 초안만 남기고 실제 문서 반영을 미루는 방식은 보조 수단으로만 사용한다.
- 영향 문서가 있으면 같은 브랜치와 같은 PR 범위에서 함께 수정해 정합성을 맞춘다.
- 정합성 판단 기준은 수정 중인 워킹트리가 아니라 확인 가능한 `branch + commit`, diff, 반영 문서 목록 기준으로 설명한다.
- 불확실성이 큰 변경은 먼저 wiki 이슈나 짧은 초안으로 범위를 고정한 뒤 실제 문서를 수정한다.

## 줄바꿈 기준
- 텍스트 파일의 줄바꿈 기준은 `.gitattributes`를 따른다.
- 특별한 예외가 없으면 텍스트 파일은 `LF`로 작성한다.
- 줄바꿈 혼합(`mixed`) 상태가 보이면 같은 작업 범위에서 정규화한다.

## 문서 원문 읽기 기본값
- 커밋된 한글 Markdown 원문은 원칙적으로 `git show <ref>:<repo-relative-path>`로 먼저 읽는다.
- `<ref>`가 불명확하면 먼저 이번 판단의 기준 `branch + commit`을 확정한다.
- 이유: 현재 PowerShell 출력 인코딩 환경에서는 한글 문서가 깨질 수 있고, 처음부터 Git 객체를 읽는 편이 기준 commit 일관성과 토큰 사용 면에서도 더 효율적이다.
- 한글 문서를 확인할 때는 PowerShell 기본 출력 인코딩에 의존하지 않는다.
- `Get-Content`, `Select-String`, 기타 파일 시스템 읽기는 미커밋 변경, 신규 파일, 워킹트리 상태 확인이 필요할 때만 fallback으로 사용한다.
- fallback 파일 읽기가 필요하면 `Get-Content -Encoding utf8`처럼 UTF-8을 명시한 방식만 사용한다.
- 출력 인코딩을 임시로 바꿔가며 여러 번 재시도하는 방식은 기본 경로로 쓰지 않는다.
- 같은 턴에서 이미 `git show`로 읽은 커밋 문서를 PowerShell 파일 읽기로 다시 중복 확인하지 않는다.
- 필요한 경우에도 전체 파일 재읽기보다 필요한 섹션만 좁혀 읽는다.
- 커밋 기준 본문과 워킹트리 본문을 함께 사용했으면 둘을 구분해서 설명한다.

## `git show` 사용 기준 표

| 상황 | 기본 확인 방식 | fallback | 메모 |
| --- | --- | --- | --- |
| 커밋된 한글 문서 원문 확인 | `git show <ref>:<path>` | 없음 | 먼저 기준 `branch + commit`을 확정한다. |
| 같은 커밋 문서의 특정 섹션 재확인 | `git show <ref>:<path>` 후 필요한 섹션만 확인 | 없음 | 같은 턴에서 PowerShell 파일 읽기로 다시 확인하지 않는다. |
| 미커밋 변경 확인 | `git diff -- <path>` | 파일 시스템 읽기 | baseline이 아니라 워킹트리 상태로 취급한다. |
| 신규 untracked 파일 확인 | 파일 시스템 읽기 | 없음 | Git 객체에 아직 없으므로 `git show` 대상이 아니다. |
| 워킹트리 전체 상태 확인 | `git status` | 파일 시스템 읽기 | 커밋 기준 내용과 섞지 말고 별도로 설명한다. |

## raw / source 규칙
- `raw/`는 원본 또는 원본 참조 계층이다.
- `raw/`에는 해석, 판단, 우선순위를 적지 않는다.
- `raw/issues`
  - GitHub issue 원문 메타데이터 기준
- `raw/prs`
  - GitHub PR 메타데이터 + merge commit 기준
- `05-Sources`
  - 사실만 적는다.
  - 해석은 `01-Project`, `02-Architecture`, `03-Status`, `04-Records`에 적는다.

## 개인 로컬 경로 설정
- 공용 문서에는 개인 로컬 경로를 적지 않는다.
- 각 사용자는 `raw/repos/_repo-local-card.template.md`를 참고해 `raw/repos/{repo}.local.md`를 만든다.
- 이 파일에는 `execution_path` 같은 실행 경로 메타데이터를 기록한다.
- `{repo}.local.md`는 gitignored 파일이므로 원격 저장소에 올라가지 않는다.
- 프로젝트 세션용 wiki 경로는 프로젝트 저장소의 `./.local/wiki-repo.yml`에 기록한다.
- 이 파일은 프로젝트 저장소에서 gitignored 로컬 설정 파일로 관리한다.
- 현재 shell이 WSL이면 `wiki_repo_paths.wsl`, Windows shell이면 `wiki_repo_paths.windows`를 쓴다.
- 현재 shell 슬롯 값이 없거나 현재 세션에서 접근할 수 없으면 사용자에게 경로를 한 번만 확인하고, 같은 파일의 현재 shell 슬롯에 저장한 뒤 이후 기본값으로 재사용한다.

## 프로젝트 세션 연계 규칙
- 프로젝트 세션에서 local wiki 저장소를 참조하는 것을 기본 환경으로 본다.
- 기본 작업 컨텍스트는 프로젝트 저장소 세션이다.
- 사용자는 프로젝트 세션에서 로컬 wiki를 읽고 현재 상태, 다음 작업, 근거 문서를 확인한다.
- 연결된 wiki 저장소 문서 해석과 요청 해석 규칙의 기준 진실은 프로젝트 저장소의 `AGENTS.md`에 둔다.
- 프로젝트 저장소의 `AGENTS.md`는 wiki 경로 bootstrap과 `저장소 최신 여부 확인` / `문서 반영 점검` 요청 분기를 담당한다.
- wiki 저장소 루트 `AGENTS.md`는 이 저장소에 직접 들어왔을 때의 entry 규칙과 전역 기본값만 담당한다.
- `wiki/Home/Wiki-Usage-Guide.md`는 사람이 의도를 더 정확히 전달하기 위한 예시 문서로만 사용한다.
- local wiki 저장소 경로를 확인할 때는 먼저 프로젝트 저장소의 `./.local/wiki-repo.yml`을 본다.
- 현재 shell이 WSL이면 `wiki_repo_paths.wsl`, Windows shell이면 `wiki_repo_paths.windows`를 확인한다.
- 현재 shell 슬롯 값이 있고 현재 세션에서 접근 가능하면 그 경로를 이번 세션의 기본 wiki 경로로 사용한다.
- 현재 shell 슬롯 값이 없거나 현재 세션에서 접근할 수 없으면 자동 추정하지 말고 사용자에게 경로를 한 번만 확인한 뒤, 같은 파일의 현재 shell 슬롯에 저장하고 이후 기본값으로 사용한다.
- 프로젝트 세션의 shell에서 실제로 접근 가능한 경로를 써야 한다. 프로젝트 `execution_path`가 WSL이면 wiki 경로도 WSL에서 보이는 경로를 쓴다.
- `raw/repos/{repo}.local.md`는 wiki 경로 bootstrap 1차 기준이 아니라 `execution_path` 같은 보조 로컬 메타데이터용으로만 사용한다.
- 프로젝트 코드 확인, 구현, 검증은 프로젝트 저장소에서 수행하고, wiki 저장소는 문서 반영 브랜치와 공유 문서 관리 용도로만 사용한다.
- wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 모두 wiki 저장소에서 수행한다. 프로젝트 저장소에서는 반영 범위만 정리하고 실제 git 작업은 하지 않는다.
- 프로젝트 세션에서 여러 요청을 이어 처리할 때도, 새 요청 시작 전과 중요한 판단 단계 전에는 `git fetch origin main`으로 기준 `origin/main` 최신 ref를 다시 확인한다.
- 환경 변수나 shell 초기화 파일 설정은 필수로 두지 않는다.
- 프로젝트 작업이 끝나고 브랜치 PR이 완료되면, 사용자는 같은 프로젝트 세션에서 `지금 완료된 작업 wiki에 등록해줘.`처럼 짧게 wiki 등록을 요청할 수 있다.

## 브랜치 최신 확인과 문서 반영 점검 구분
- `wiki 저장소 최신이야?` 같은 요청은 기본적으로 연결된 wiki 저장소의 원격 기준 최신 여부 확인으로 본다.
- `최근 프로젝트 변경사항이 wiki 문서에 반영됐는지`, `문서 내용 기준으로`, `코드와 wiki를 대조해서`, `누락 항목까지` 같은 요청은 저장소 최신 여부가 아니라 문서 반영 점검으로 본다.
- 문서 반영 점검은 프로젝트의 확정된 `code@commit` 기준과 wiki의 `origin/main@<hash>` 기준 문서를 비교하는 작업이다.
- 문서 반영 점검 요청을 브랜치 최신 여부 확인만으로 좁혀 해석하지 않는다.

## AGENTS 읽기 운영 원칙
- 루트 `AGENTS.md`는 저장소 세션 시작 시 1회 읽는 기본 규칙 문서로 본다.
- `wiki/AGENTS.md`는 같은 세션에서 처음으로 wiki 작업 범위에 들어갈 때 1회 읽는다.
- 같은 세션에서 이미 읽은 `AGENTS.md` 계열 문서는 매 요청마다 전체를 다시 읽지 않는다.
- 단순 후속 요청이나 같은 작업 흐름에서는 이미 확인한 AGENTS 규칙을 세션 기준값으로 재사용한다.
- 다시 읽기가 필요한 경우는 저장소 변경, 브랜치 변경, 규칙 변경 요청, 작업 범위 이동, 현재 세션에서 `AGENTS.md` 계열 문서를 수정한 경우, 규칙 충돌이나 해석 불확실성으로 판단이 막히는 경우로 한정한다.
- sync 상태, 원격 branch, 현재 인증 상태처럼 시간에 따라 바뀔 수 있는 정보는 필요할 때 다시 확인하되, 그때마다 `AGENTS.md` 전체 재읽기를 기본 경로로 쓰지 않는다.

## wiki 사용법 질문 응답 기준
- 사용자가 `wiki를 어떻게 사용하냐`, `wiki에서 뭐 물어볼 수 있냐`, `wiki 어떻게 봐야 하냐`고 물으면 문서 링크만 나열하지 말고 세션에서 바로 복사해 쓸 수 있는 짧은 요청문을 먼저 3~8개 제시한다.
- 요청 예시는 상태 확인, 주제 확인, 근거 문서 찾기, 설계 이유 확인, wiki 등록 요청을 고르게 포함한다.
- 요청 예시에는 저장소 최신 여부 확인과 문서 반영 점검 문장을 구분해서 포함한다.
- 관련 문서 링크는 그 다음에 `wiki/Home/Wiki-Usage-Guide.md`, `wiki/Home/README.md`, `wiki/Home/Wiki-Operating-Rules.md` 순서로 보강한다.

## 간단한 wiki 등록 요청 처리 기준
- 사용자가 `지금 완료된 작업 wiki에 등록해줘.`라고 요청하면, 문서 경로나 반영 절차를 다시 하나씩 묻기보다 현재 프로젝트 세션의 최신 완료 작업 기준 wiki 등록 요청으로 해석한다.
- 가능하면 기준 프로젝트 PR/merge commit 또는 방금 완료한 작업 범위를 먼저 확정한다.
- 기준이 확정되면 `05-Sources`, `03-Status`, 필요 시 `04-Records`, `log.md`, `index.md` 반영 여부를 먼저 정리한다.
- 사용자는 반영 대상 문서를 일일이 지정할 필요가 없다. 범위를 제한하고 싶을 때만 추가 조건을 준다.
- 기준이 모호하면 그때만 최소 질문으로 기준 PR/commit 또는 반영 범위를 확인한다.
- 이후 실제 브랜치 생성, 문서 수정, PR 준비는 아래 publish 규칙과 사용자 동의 절차를 따른다.

## 프로젝트 PR wiki 반영 체크리스트
1. 기준 프로젝트 `repo / branch / PR 번호 / merge commit`을 확인한다.
2. 이번 PR로 바뀐 기능과 모듈에 대응하는 `05-Sources/` 문서를 확인하거나 갱신한다.
3. 완료된 사실과 현재 기준 상태를 `03-Status/Current-State.md`에 반영한다.
4. 다음 우선 작업, 선행조건, 남은 gap 변화를 `03-Status/Next-Work.md`에 반영한다.
5. 결정, 이슈, 작업 경과를 남길 가치가 있으면 `04-Records/`를 갱신한다.
6. 새 문서 추가, 삭제, 이름 변경이 있으면 `index.md`를 갱신한다.
7. 의미 있는 반영 단위면 `log.md`를 기록한다.
8. raw PR/source card를 새로 확보해야 하면 `raw/prs/`와 관련 source 문서를 함께 확인한다.

## `<topic-slug>` 규칙
- 소문자 영어, 숫자, 하이픈만 사용한다.
- kebab-case로 적고 2~6단어 정도로 유지한다.
- `docs`, `pr`, `branch`, `update`, `misc`, 날짜, PR 번호처럼 prefix에서 이미 드러나는 정보는 slug에 반복하지 않는다.
- 너무 포괄적인 이름보다 반영 주제나 기능 단위를 직접 드러내는 명사를 우선한다.
- 예: `wiki-sync-workflow`, `history-panel-docs`, `round-summary-records`

## 이슈 생성 기준
- 프로젝트 코드 관련 이슈는 대상 코드 repo의 GitHub issue template을 따른다.
- wiki 저장소 자체 이슈는 wiki 저장소 전용 변경 이슈 template을 따른다.
- 프로젝트 이슈와 wiki 이슈는 서로 다른 저장소 규칙으로 보고 template을 혼용하지 않는다.
- 이슈 생성 요청만으로는 작업 브랜치를 자동 생성하지 않는다.

## 간단한 GitHub 작업 처리 원칙
- `이슈 생성`, `작업 브랜치 생성`, `이슈 + 작업 브랜치 준비` 같은 단순 GitHub 작업은 빠른 경로로 처리한다.
- 기본 확인 범위는 대상 저장소, 해당 template, 원격 기준 branch 확인에 한정한다.
- 같은 세션에서 이미 확인한 규칙과 상태는 반복 조회하지 않는다.
- 전체 wiki 읽기나 관련 없는 문서 재확인은 blocker가 있을 때만 수행한다.
- 특별한 오류, 승인 대기, 원격 장애가 없으면 단순 GitHub 작업은 1~2분 안쪽 처리를 기본 목표로 한다.

## wiki 변경 이슈 template
- wiki 저장소 변경 이슈는 `.github/ISSUE_TEMPLATE/wiki-change-template.md`를 기준으로 작성한다.
- 규칙/가이드/운영 문서 변경 이슈 제목은 기본적으로 `docs: <주제>` 형식을 사용한다.
- 기본 섹션은 `배경`, `목적`, `작업 범위`, `확인 기준`, `비고` 순서다.
- `작업 범위`에는 포함할 항목과 제외할 항목을 함께 적는다.
- `확인 기준`에는 문서명과 반영 상태가 드러나는 검증 가능한 조건을 적는다.
- `확인 기준`에는 반영할 규칙 문서와 함께 동기화할 사용자 문서가 있으면 그 문서명과 기대 상태를 함께 적는다.
- 요청 방식이나 승인 흐름이 바뀌는 변경이면 `wiki/Home/Wiki-Usage-Guide.md`에 추가할 예시 요청도 확인 기준에 포함한다.
- `비고`에는 참고 링크, 예외, 보류 사항, 열린 질문을 적는다.

## 이슈 / PR 작성 언어
- 새로 작성하는 GitHub `issue` 제목/본문, `PR` 제목/본문, 변경 요약은 기본적으로 한글로 작성한다.
- 다른 언어는 사용자가 명시적으로 요청한 경우에만 사용한다.
- 원문 메타데이터나 외부 원문 인용은 source 기준을 유지하되, 새로 작성하는 설명과 요약은 한글을 기본으로 한다.
- PowerShell 환경에서는 한글 `issue`/`PR` 본문을 stdin이나 here-string 파이프로 직접 넘기지 않는다.
- 한글 본문이 필요하면 UTF-8로 저장된 파일을 만들고 `gh ... --body-file <utf8-file>`처럼 파일 기반으로 전달한다.
- 본문이 `??`처럼 깨져 올라갔으면 인코딩 문제로 보고, 같은 내용을 UTF-8 파일 기반으로 다시 업로드한다.

## PR 제목 / 본문 형식
- 연결할 같은 저장소 이슈가 있으면 `비고`에 `Closes #<번호>` 또는 `Refs #<번호>`를 함께 적는다.
- wiki 규칙/가이드/운영 문서 수정 PR 제목은 `docs: <주제>`를 사용한다.
- 프로젝트 PR 반영 PR 제목은 `pr: <project-pr-number> <주제>`를 사용한다.
- `docs` PR 본문은 `변경 요약 -> 반영 문서 -> 비고` 순서를 사용한다.
- `pr` PR 본문은 `기준 작업 -> 변경 요약 -> 반영 문서 -> 비고` 순서를 사용한다.
- `기준 작업`에는 프로젝트 PR 번호와 기준 `branch + commit`을 적는다.
- `반영 문서`에는 실제로 갱신한 wiki 문서만 적는다.
- `비고`에는 남은 작업, 제외 범위, 리뷰 포인트만 짧게 적는다.

## 작성 규칙
- 새 페이지보다 기존 페이지 업데이트를 우선한다.
- 이유: 같은 역할의 문서가 여러 개 생기면 단일 진실 원본이 깨지고, 사람과 LLM 모두 어떤 문서를 봐야 하는지 헷갈리기 때문이다.
- 새 문서는 아래 경우에만 만든다.
  - 기존 문서와 역할이 명확히 다른 새 산출물이 필요할 때
  - 기존 문서가 과도하게 비대해져 최소 단위로 분리할 필요가 있을 때
  - source / worklog / decision처럼 문서 단위 식별이 필요한 기록일 때
- 모든 공식 wiki 문서는 YAML frontmatter를 포함한다.
- 단, `AGENTS.md` 계열 운영 규칙 파일은 예외로 한다.
- 이유: `AGENTS.md`는 산출물 페이지가 아니라 LLM 행동 규칙 파일이므로, 일반 문서와 같은 메타데이터 규칙을 강제하지 않는다.
- wiki 내부 링크는 wikilink만 사용한다.

## frontmatter 최소 규칙
모든 공식 wiki 문서:

```yaml
---
title:        # 문서 이름
type:         # 문서 종류
status:       # active, draft, partial, archived 등
updated:      # 마지막 갱신 날짜
tags:         # 검색 / 분류 태그
---
```

소스 문서 추가 필드:

```yaml
source_kind:  # repo / issue / pr
source_ref:   # 원본 식별자
commit:       # 근거 commit hash
```

## index / log 규칙
- `index.md`
  - 새 문서 생성 / 삭제 시 반드시 갱신
  - 제목, 경로, 문서 역할, 카탈로그 요약이 바뀌면 갱신
  - 본문 보강만 한 경우 생략 가능
- `log.md`
  - ingest / backfill / 구조 변경 / 상태 변경 / 규칙 변경처럼 의미 있는 업데이트 단위만 기록
  - git commit 여부와 별개로, wiki 기준이나 문서 의미가 바뀌면 기록 가능
  - 오탈자 수정, 표현 다듬기, 문장 순서 조정처럼 의미 변화가 없는 자잘한 수정은 기록하지 않음
  - 같은 주제의 작은 수정은 한 번의 로그 엔트리로 묶음

## ingest 순서
1. `git fetch origin main`으로 기준 `origin/main@<hash>`를 확인
2. 대상 `repo / branch / commit hash` 확정
3. raw 참조 카드 갱신 또는 확인
4. 코드 / issue / PR 읽기
5. `05-Sources` 갱신
6. 필요 시 `02-Architecture` 갱신
7. 필요 시 `03-Status` 갱신
8. 필요 시 `04-Records` 갱신
9. 필요 시 `index.md` 갱신
10. 의미 있는 업데이트 단위면 `log.md` 기록

## LLM 기본 읽기 순서
- 사용자가 `wiki 읽고 내용 확인해`, `wiki 보고 정리해`, `wiki 기준으로 말해줘`라고 하면 아래 순서로 먼저 읽는다.
  1. `git fetch origin main`으로 최신 상태를 확인하고 기준 `origin/main@<hash>`를 확정한다.
  2. 커밋된 문서는 원칙적으로 `git show <ref>:<path>`로 원문을 읽는다.
  3. `wiki/index.md`
  4. `wiki/Home/README.md`
  5. `wiki/03-Status/Current-State.md`
  6. `wiki/03-Status/Next-Work.md`
- 그 다음 질문 목적에 따라 확장한다.
  - 프로젝트 정의 질문:
    1. `wiki/01-Project/README.md`
  - 구조 질문:
    1. `wiki/02-Architecture/System-Reference.md`
    2. 필요 시 `wiki/02-Architecture/Data-Flow.md`
    3. 필요 시 `wiki/05-Sources/`
  - 결정 / 이유 질문:
    1. `wiki/04-Records/Decisions/`
    2. 필요 시 `wiki/04-Records/Issues/`
    3. 필요 시 `wiki/05-Sources/`
- wiki에 없는 내용은 추측하지 않는다.
- 필요할 때만 마지막 수단으로 `raw/`를 읽는다.

## future issue / PR 규칙
- 앞으로 생기는 issue / PR은 모두 `raw/`에 먼저 기록한다.
- 새로 생성하는 GitHub `issue`/`PR` 제목, 본문, 설명, 요약은 기본적으로 한글로 작성한다.
- 현재 상태를 바꾸는 작업이면 `03-Status/Current-State.md`를 항상 갱신한다.
- 다음 작업 우선순위를 바꾸는 작업이면 `03-Status/Next-Work.md`를 항상 갱신한다.
- `05-Sources`와 `04-Records`는 재사용 가치가 있을 때만 선별 승격한다.

## 규칙 변경 시 사용자 문서 동기화
- `AGENTS.md` 계열, wiki 운영 절차, publish 절차, 요청 방식 관련 규칙을 바꾸면 `wiki/Home/Wiki-Operating-Rules.md`와 `wiki/Home/Wiki-Usage-Guide.md`를 함께 검토한다.
- 팀 운영 설명이나 절차가 바뀌면 `wiki/Home/Wiki-Operating-Rules.md`를 업데이트한다.
- 사람용 요청 예시, 사용 흐름, LLM 호출 가이드가 바뀌면 `wiki/Home/Wiki-Usage-Guide.md`를 업데이트한다.
- 둘 다 영향이 있으면 같은 브랜치와 같은 PR 범위에서 함께 수정한다.
- `AGENTS.md` 계열과 사용자 문서가 충돌하면 `AGENTS.md` 계열을 기준 진실로 보고, 같은 브랜치와 같은 PR 범위에서 사용자 문서를 함께 정정한다.
- 변경된 규칙이 사용자 요청 문장, 승인 흐름, 작업 순서 예시에 영향을 주면 `wiki/Home/Wiki-Usage-Guide.md`에 예시 요청을 최소 1개 함께 추가한다.
- 영향이 없어 사용자 문서 수정을 생략하면 변경 요약이나 PR 본문 `비고`에 사유를 짧게 남긴다.

## 규칙 변경 PR 체크 항목
- PR이 같은 저장소의 이슈를 완전히 해결하면 `비고`에 `Closes #<번호>`를 적는다.
- 관련은 있지만 완전히 닫지 않으면 `Closes` 대신 `Refs #<번호>`를 적는다.
- wiki 규칙/가이드/운영 문서 수정 PR의 `비고`에는 `사용자 문서 동기화 여부`, `issue/template 변경 여부`, `생략 사유`를 짧게 적는다.
- `Wiki-Usage-Guide.md`에 예시 요청을 추가했다면 어떤 예시를 추가했는지 `비고`에 함께 적는다.
- 사용자 문서 수정이나 template 변경이 없으면 `없음`과 사유를 분명히 적는다.

## publish 규칙
1. 프로젝트 브랜치 PR이 완료되고 사용자가 wiki 등록을 요청하면, 같은 프로젝트 세션에서 기준 프로젝트 PR/merge commit과 반영 범위를 먼저 정리한다. `지금 완료된 작업 wiki에 등록해줘.` 같은 짧은 요청도 여기에 포함한다.
2. wiki 반영 직전에는 `git fetch origin main`으로 기준 `origin/main@<hash>`를 다시 확인한다.
3. wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 모두 wiki 저장소에서 수행한다. 프로젝트 저장소에서 wiki 반영 브랜치를 만들지 않는다.
4. wiki 반영은 direct push가 아니라 `branch + PR` 기준으로 운영한다.
5. wiki 반영 브랜치는 기본적으로 `docs/<topic-slug>`를 사용한다.
6. 특정 프로젝트 PR에 대응하는 반영이면 `pr/<project-pr-number>-<topic-slug>` 형식을 사용한다.
7. `<topic-slug>`는 위 slug 규칙을 따른다.
8. 프로젝트 PR 반영이면 위 체크리스트 기준으로 wiki 내용을 먼저 작성 / 갱신한다.
9. 변경 내용 요약, `PR` 제목/본문, 관련 `issue` 초안이 필요하면 위 언어 규칙과 `PR 제목 / 본문 형식`에 따라 한글로 정리한다.
   - PowerShell에서는 한글 본문을 stdin으로 넘기지 않고 UTF-8 파일 기반으로 작성한다.
10. `커밋할까?`라고 사용자 동의를 받는다.
11. 동의가 있으면 로컬 커밋을 진행한다.
12. 커밋 후 PR용 변경 요약을 정리한다.
13. `PR 요청할까?`라고 사용자 동의를 받는다.
14. 동의가 있을 때만 push / PR 생성을 진행한다.
15. wiki `main` 머지도 사용자 동의와 검토를 전제로 진행한다.
- `log.md` 기록과 git commit은 별개다.
- `log.md`는 의미 있는 wiki 변경을 남기고, git commit은 사용자 동의 후에만 진행한다.

## 한 줄 요약
- `05-Sources`에는 사실만 적는다.
- `03-Status`에는 현재 사실과 다음 행동을 적는다.
- `04-Records`에는 작업, 문제, 결정을 축적한다.
- wiki는 항상 `code@commit` 기준으로 읽고 쓰며, 사용 전에는 `git fetch origin main`으로 `origin/main@<hash>`를 기준 ref로 확정한다.
