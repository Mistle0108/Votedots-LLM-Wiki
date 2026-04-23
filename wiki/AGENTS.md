## 목적
- `wiki/`는 Votedots 프로젝트의 **공식 문서와 산출물**을 관리하는 계층이다.
- LLM은 `wiki/`를 읽고 아래를 빠르게 답할 수 있어야 한다.
  - 프로젝트가 무엇인지
  - 지금 어디까지 됐는지
  - 다음에 무엇을 해야 하는지
  - 왜 그렇게 작업/결정했는지
- 사용자는 주로 프로젝트 저장소 세션에서 wiki를 읽고 작업 방향을 잡으며, wiki 등록 요청도 같은 세션에서 시작한다.
- `wiki/Home/Wiki-Usage-Guide.md`는 사람용 요청 예시 문서다. LLM 실행 규칙이 필요하면 항상 `AGENTS.md` 계열 문서를 우선한다.

## 구조
```text
Home/             # 진입점, 읽는 순서, 핵심 링크
01-Project/       # 프로젝트 정의
02-Architecture/  # 시스템 구조, 데이터 흐름, 운영 아키텍처
03-Status/        # 현재 상태, 다음 작업
04-Records/       # 작업 기록, 문제, 결정
05-Sources/       # repo / issue / PR 사실 요약
index.md          # 전체 문서 카탈로그
log.md            # wiki 운영 이력
```

## 핵심 원칙
- `wiki/` 문서는 항상 특정 `branch + commit` 기준으로 읽고 쓴다.
- 기준 진실은 항상 `code@commit`이다.
- 미커밋 변경은 baseline에 포함하지 않는다.
- `03-Status/Current-State.md`는 현재 상태의 단일 진실 원본이다.
- `03-Status/Next-Work.md`는 다음 작업의 단일 진실 원본이다.
- `05-Sources/`에는 사실만 적고, 해석은 `01-Project`, `02-Architecture`, `03-Status`, `04-Records`에 적는다.
- 새 페이지보다 기존 페이지 업데이트를 먼저 검토한다.
- 모든 공식 wiki 문서는 YAML frontmatter를 포함한다.
- 단, `AGENTS.md` 계열 운영 규칙 파일은 예외로 한다.
- 이유: `AGENTS.md`는 산출물 페이지가 아니라 LLM 행동 규칙 파일이므로, 일반 문서와 같은 메타데이터 규칙을 강제하지 않는다.
- `index.md`는 문서 목록과 탐색 구조를 관리하고, `log.md`는 의미 있는 업데이트 이력을 관리한다.
- 사용자의 명령을 wiki 기준으로 수행하기 전에는 먼저 `git fetch origin main`으로 원격 최신 상태를 확인한다.
- `git fetch`가 성공하면 `git rev-parse origin/main`으로 `origin/main@<hash>`를 이번 작업 기준으로 확정한다.
- 원격 확인이 불가능하면 최신이라고 단정하지 말고 제한과 마지막으로 확인 가능한 기준 `branch + commit`을 먼저 밝힌다.

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
- 커밋 기준 본문과 워킹트리 본문을 함께 읽었으면 둘을 섞어 말하지 말고 구분해서 설명한다.

## `git show` 사용 기준 표

| 상황 | 기본 확인 방식 | fallback | 메모 |
| --- | --- | --- | --- |
| 커밋된 한글 문서 원문 확인 | `git show <ref>:<path>` | 없음 | 처음부터 안 깨지는 경로로 읽는다. 먼저 기준 `branch + commit`을 확정한다. |
| 같은 커밋 문서의 특정 섹션 재확인 | `git show <ref>:<path>` 후 필요한 섹션만 확인 | 없음 | 같은 턴에서 PowerShell 파일 읽기로 다시 확인하지 않는다. |
| 미커밋 변경 확인 | `git diff -- <path>` | 파일 시스템 읽기 | baseline이 아니라 워킹트리 상태로 취급한다. 파일 시스템 읽기가 필요하면 UTF-8을 명시한다. |
| 신규 untracked 파일 확인 | 파일 시스템 읽기 | 없음 | Git 객체에 아직 없으므로 `git show` 대상이 아니다. UTF-8을 명시한다. |
| 워킹트리 전체 상태 확인 | `git status` | 파일 시스템 읽기 | 커밋 기준 내용과 섞지 말고 별도로 설명한다. |

## 작업 전 최신화 확인 원칙
- wiki 기준으로 읽기/쓰기/판단/등록 작업을 시작하기 전에는 항상 `git fetch origin main`으로 원격 최신 상태를 먼저 확인한다.
- `git fetch`가 성공하면 `git rev-parse origin/main`으로 `origin/main@<hash>`를 이번 작업 기준으로 확정하고 진행한다.
- 커밋 기준 문서 읽기와 판단은 원칙적으로 이 `origin/main@<hash>` 기준으로 수행한다.
- 로컬 `main` 상태는 최신 기준 확정의 필수 조건으로 두지 않는다.
- `git fetch`가 실패하거나 `origin/main` 해시를 읽지 못하면 최신이라고 단정하지 않고, 실패 사유와 마지막으로 확인 가능한 기준 `branch + commit`만 먼저 공유한다.
- 자동 `pull`, `merge`, `rebase`, 강제 `reset`은 하지 않는다.

## 원격 최신 확인 절차
1. 기본 명령 순서는 `git fetch origin main` -> `git rev-parse origin/main` 이다.
2. 두 명령이 성공하면 `origin/main@<hash>`를 이번 읽기/쓰기 기준으로 확정한다.
3. 커밋된 문서는 원칙적으로 `git show origin/main:<path>` 또는 확정된 `git show <ref>:<path>` 기준으로 읽는다.
4. `git fetch`가 실패하면 최신이라고 단정하지 않고, 실패 사유와 마지막으로 확인 가능한 기준 `branch + commit`만 먼저 밝힌다.
5. `origin/main` 해시를 읽지 못하면 현재 세션에서 최신 기준 ref를 확정하지 못했다는 사실을 먼저 밝힌다.
6. 긴 작업 중 새 사용자 명령이나 중요한 판단 직전에는 이 절차를 다시 수행한다.

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

## 프로젝트 세션 연계 규칙
- 프로젝트 세션에서 local wiki 저장소를 참조하는 것을 기본 환경으로 본다.
- 프로젝트 작업을 위해 wiki를 읽거나 wiki 등록을 준비할 때는 프로젝트 저장소의 `execution_path` 기준 세션에서 진행한다.
- 프로젝트 세션에서 local wiki 저장소 경로를 확인할 때는 먼저 프로젝트 저장소의 `./.local/wiki-repo.yml`을 본다.
- 현재 shell이 WSL이면 `wiki_repo_paths.wsl`, Windows shell이면 `wiki_repo_paths.windows`를 본다.
- 현재 shell 슬롯 값이 있고 현재 세션에서 접근 가능하면 그 경로를 이번 세션의 기본 wiki 경로로 고정한다.
- 현재 shell 슬롯 값이 없거나 현재 세션에서 접근할 수 없으면 자동 추정하지 말고 사용자에게 경로를 한 번만 확인한다.
- 확인한 경로는 같은 파일의 현재 shell 슬롯에 저장하고 이후 기본값으로 재사용한다.
- 프로젝트 세션의 shell에서 실제로 접근 가능한 경로를 써야 한다. 프로젝트 `execution_path`가 WSL이면 wiki 경로도 WSL에서 보이는 경로를 쓴다.
- 프로젝트 세션에서는 로컬 wiki를 참조 문서로 읽고, 각 사용자 명령과 중요한 판단 단계 전에 `git fetch origin main`으로 기준 `origin/main` 최신 ref를 다시 확인한다.
- 프로젝트 저장소 경로가 필요하면 `raw/repos/{repo}.local.md`의 `execution_path`를 먼저 확인하고, 없으면 세션 입력으로 받는다.
- 같은 세션에서 이미 한 번 확인한 wiki repo 경로가 있으면 다시 묻지 않고 그 값을 계속 사용한다.
- `raw/repos/{repo}.local.md`는 wiki repo 경로 bootstrap 1차 기준으로 쓰지 않는다.
- 프로젝트 코드 확인, 설계, 구현, 검증은 프로젝트 저장소에서 수행하고, wiki 저장소는 문서 반영 브랜치와 공유 문서 관리 용도로만 사용한다.
- wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 모두 wiki 저장소에서 수행한다. 프로젝트 저장소에서는 반영 범위만 정리하고, 실제 git 작업은 wiki 저장소 기준으로 진행한다.
- 환경 변수나 shell 초기화 파일 설정은 필수로 두지 않는다.
- 프로젝트 브랜치 PR이 완료된 뒤 사용자가 wiki 등록을 요청하면, 먼저 프로젝트 PR/merge commit 기준으로 반영 범위를 정리한다.

## LLM 기본 읽기 순서
- 사용자가 `wiki 읽고 내용 확인해`, `wiki 보고 정리해`, `wiki 기준으로 말해줘`라고 하면 아래 순서로 먼저 읽는다.
  1. `git fetch origin main`으로 원격 최신 상태를 확인하고, 이번 답변의 기준 `origin/main@<hash>`를 확정한다.
  2. 프로젝트 연계 질문이면 프로젝트 저장소 `execution_path`, 현재 실행 컨텍스트, 프로젝트 저장소의 `./.local/wiki-repo.yml` 현재 shell 슬롯 또는 같은 세션에서 이미 확인한 wiki repo 경로를 확인한다.
  3. 커밋된 문서는 원칙적으로 `git show <ref>:<path>`로 원문을 읽는다.
  4. `wiki/index.md`
  5. `wiki/Home/README.md`
  6. `wiki/03-Status/Current-State.md`
  7. `wiki/03-Status/Next-Work.md`
- 그 다음 질문 유형에 따라 확장한다.
  - 프로젝트 정의 질문:
    1. `wiki/01-Project/README.md`
  - 구조 질문:
    1. `wiki/02-Architecture/System-Reference.md`
    2. 필요 시 `wiki/02-Architecture/Data-Flow.md`
    3. 필요 시 `wiki/05-Sources/`
  - 상태 질문:
    1. 필요 시 `wiki/04-Records/`
  - 결정 / 이유 질문:
    1. `wiki/04-Records/Decisions/`
    2. 필요 시 `wiki/04-Records/Issues/`
    3. 필요 시 `wiki/05-Sources/`

## AGENTS 재읽기 기준
- `wiki/AGENTS.md`는 같은 세션에서 처음으로 wiki 작업 범위에 들어갈 때 1회 읽는 것을 기본으로 한다.
- 같은 세션에서 이미 읽은 뒤에는 새 요청마다 `wiki/AGENTS.md` 전체를 다시 읽지 않는다.
- 단순 후속 요청, 같은 wiki 작업 흐름, 이미 같은 세션에서 확인한 GitHub 작업 처리에는 세션에 캐시된 AGENTS 규칙을 재사용한다.
- 다시 읽기가 필요한 경우는 브랜치 변경, 저장소 변경, 사용자가 규칙 변경을 요청한 경우, 작업 범위가 wiki 밖 또는 다른 규칙 영역으로 넘어갔다가 다시 들어온 경우, 현재 세션에서 `AGENTS.md` 계열 문서를 수정한 경우, 규칙 충돌이나 해석 불확실성으로 현재 판단이 막히는 경우로 한정한다.
- `git fetch`, `origin/main`, 현재 브랜치, 인증 상태처럼 시간에 따라 바뀔 수 있는 정보는 필요할 때 다시 확인하되, 그 확인을 이유로 `wiki/AGENTS.md` 전체를 재읽지 않는다.
- 빠른 경로 대상인 단순 GitHub 작업에서는 `AGENTS.md` 재탐색보다 세션 기준 규칙 재사용을 우선한다.

## LLM 응답 원칙
- wiki를 읽기 전에 기억만으로 답하지 않는다.
- wiki에 없는 내용은 추측하지 않는다.
- wiki로 답하기 부족하면 어떤 문서가 부족한지 먼저 말한다.
- 필요할 때만 `raw/`를 마지막 수단으로 읽는다.
- `git fetch origin main`으로 기준 ref를 확인하지 못했으면 최신 기준이라고 단정하지 않는다.
- wiki를 근거로 현재 상태나 다음 작업을 말할 때는 기준 `branch + commit` 또는 확인 실패 사유를 먼저 밝힌다.
- 커밋 기준 본문과 워킹트리 본문을 함께 썼으면 어떤 부분이 어느 기준인지 구분해서 설명한다.
- 사람용 안내 문서와 LLM 규칙 문서가 동시에 보이면, LLM은 항상 `AGENTS.md` 계열 규칙을 우선한다.
- 커밋된 한글 문서 원문 확인은 처음부터 Git 객체 기준으로 수행하고, fallback 사유가 없으면 PowerShell 파일 읽기로 우회하지 않는다.
- 최신 확인 결과는 `fetch 성공 -> origin/main@<hash> 확정` 또는 `fetch 실패 -> 실패 사유와 마지막 기준 상태` 순서로 짧게 설명한다.
- 프로젝트 세션에서 wiki 경로를 설명할 때는 현재 기준 wiki repo 경로와 그 경로를 어디서 확정했는지(`./.local/wiki-repo.yml` / 같은 세션 확인값)를 함께 밝힌다.

## wiki 사용법 질문 응답 원칙
- 사용자가 `wiki를 어떻게 사용하냐`, `wiki에서 뭐 물어볼 수 있냐`, `wiki 어떻게 봐야 하냐`고 물으면 `wiki/Home/Wiki-Usage-Guide.md` 기준의 세션용 요청 예시를 먼저 3~8개 제시한다.
- 요청 예시는 상태 확인, 주제 확인, 근거 문서 찾기, 설계 이유 확인, wiki 등록 요청을 고르게 포함한다.
- 문서 링크만 나열하지 말고, 사용자가 바로 복사해 쓸 수 있는 짧은 요청문을 먼저 보여준다.
- 관련 문서 링크는 그 다음에 `wiki/Home/Wiki-Usage-Guide.md`, `wiki/Home/README.md`, `wiki/Home/Wiki-Operating-Rules.md` 순서로 덧붙인다.

## 간단한 wiki 등록 요청 해석 원칙
- 사용자가 `지금 완료된 작업 wiki에 등록해줘.`라고 요청하면, 문서 경로나 반영 절차를 다시 하나씩 묻기보다 현재 프로젝트 세션의 최신 완료 작업 기준 wiki 등록 요청으로 해석한다.
- 가능하면 기준 프로젝트 PR/merge commit 또는 방금 완료한 작업 범위를 먼저 확정한다.
- 기준이 확정되면 `wiki/05-Sources/`, `wiki/03-Status/`, 필요 시 `wiki/04-Records/`, `wiki/log.md`, `wiki/index.md` 반영 여부를 먼저 정리한다.
- 사용자는 반영 대상 문서를 일일이 지정할 필요가 없다. 범위를 제한하고 싶을 때만 추가 조건을 준다.
- 기준이 모호하면 그때만 최소 질문으로 기준 PR/commit 또는 반영 범위를 확인한다.
- 이후 실제 브랜치 생성, 문서 수정, PR 준비는 아래 publish 절차와 사용자 동의 규칙을 따른다.

## 이슈 / PR 작성 언어
- 새로 작성하는 GitHub `issue` 제목/본문, `PR` 제목/본문, 변경 요약은 기본적으로 한글로 작성한다.
- 다른 언어는 사용자가 명시적으로 요청한 경우에만 사용한다.
- 원문 메타데이터나 외부 원문 인용은 source 기준을 유지하되, 새로 작성하는 설명과 요약은 한글을 기본으로 한다.
- PowerShell 환경에서는 한글 `issue`/`PR` 본문을 stdin이나 here-string 파이프로 직접 넘기지 않는다.
- 한글 본문이 필요하면 UTF-8로 저장된 파일을 만들고 `gh ... --body-file <utf8-file>`처럼 파일 기반으로 전달한다.
- 본문이 `??`처럼 깨져 올라갔으면 인코딩 문제로 보고, 같은 내용을 UTF-8 파일 기반으로 다시 업로드한다.

## 이슈 생성 기준
- 프로젝트 코드 관련 이슈는 대상 코드 repo의 GitHub issue template을 따른다.
- wiki 저장소 자체 이슈는 wiki 저장소 전용 변경 이슈 template을 따른다.
- 요청 대상이 프로젝트 repo인지 wiki repo인지 먼저 확정한 뒤 그 저장소의 template을 선택한다.
- 이슈 생성 요청만으로는 작업 브랜치를 자동 생성하지 않는다.
- 서로 다른 저장소의 issue template을 혼용하지 않는다.

## wiki 변경 이슈 template
- wiki 저장소 변경 이슈는 `.github/ISSUE_TEMPLATE/wiki-change-template.md`를 기준으로 작성한다.
- 규칙/가이드/운영 문서 변경 이슈 제목은 기본적으로 `docs: <주제>` 형식을 사용한다.
- 섹션 순서는 `배경 -> 목적 -> 작업 범위 -> 확인 기준 -> 비고`를 기본으로 사용한다.
- `배경`에는 왜 이 변경이 필요한지와 현재 혼선 또는 누락을 짧게 적는다.
- `목적`에는 이번 변경으로 만들고 싶은 최종 상태를 적는다.
- `작업 범위`에는 이번 이슈에 포함할 문서/규칙과 제외할 범위를 함께 적는다.
- `확인 기준`에는 완료 여부를 확인할 수 있는 조건을 적는다. 가능하면 문서명과 반영 상태가 드러나게 적는다.
- `확인 기준`에는 반영할 규칙 문서와 함께 동기화할 사용자 문서가 있으면 그 문서명과 기대 상태를 함께 적는다.
- 요청 방식이나 승인 흐름이 바뀌는 변경이면 `wiki/Home/Wiki-Usage-Guide.md`에 추가할 예시 요청도 확인 기준에 포함한다.
- `비고`에는 참고 링크, 보류 사항, 예외, 열린 질문을 적는다.
- LLM은 각 섹션을 짧은 bullet 위주로 채우고, 비워 둘 항목이 있으면 `- 없음`으로 명시한다.

## 작업 브랜치 생성 기준
- 작업 브랜치 생성이 필요하면 원칙적으로 `git fetch origin main` 후 `origin/main`을 직접 기준으로 새 브랜치를 만든다.
- 로컬 `main` 최신화는 작업 브랜치 생성의 필수 선행 조건으로 두지 않는다.
- 원격 확인이 실패하면 `origin/main`을 최신 기준이라고 단정하지 않고 실패 사유를 먼저 공유한다.
- 브랜치 생성 후에는 이번 작업의 기준 `branch + commit`을 함께 밝힌다.
- 브랜치명 규칙은 아래 publish 절차와 `<topic-slug>` 규칙을 따른다.

## 간단한 GitHub 작업의 빠른 처리 기준
- 이 절은 문서 수정이 없는 `이슈 생성`, `작업 브랜치 생성`, `이슈 + 작업 브랜치 준비` 요청에만 적용한다.
- LLM은 같은 세션에서 이미 확인한 저장소 대상, issue template, 브랜치 규칙, 기준 commit을 중복 조회하지 않는다.
- 다시 확인이 필요한 것은 `origin/main` 같은 원격 상태나 현재 세션의 인증 상태처럼 시간에 따라 바뀔 수 있는 정보만 한정한다.
- `이슈만` 요청이면 대상 저장소 확정과 해당 저장소 template 확인만 하고 바로 생성한다.
- `브랜치만` 요청이면 `git fetch origin main` 후 `origin/main` 기준으로 바로 생성한다.
- `이슈 + 작업 브랜치` 요청이면 template 1회 확인 -> 이슈 생성 -> `git fetch origin main` -> 브랜치 생성 순서를 기본 경로로 사용한다.
- PowerShell에서 한글 본문이 필요하면 UTF-8 파일 기반 입력만 확인하고, 그 외 문서 재탐색은 하지 않는다.
- 원격 확인 실패, 저장소 대상 불명확, template 충돌처럼 실제 blocker가 있을 때만 추가 탐색을 한다.
- 특별한 오류, 승인 대기, 원격 장애가 없으면 단순 GitHub 작업은 1~2분 안쪽 처리를 기본 목표로 한다.

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

## 규칙 변경 시 사용자 문서 동기화
- `AGENTS.md` 계열, wiki 운영 절차, publish 절차, 요청 방식 관련 규칙을 바꾸면 `wiki/Home/Wiki-Operating-Rules.md`와 `wiki/Home/Wiki-Usage-Guide.md`를 함께 검토한다.
- 팀 운영 설명이나 절차가 바뀌면 `wiki/Home/Wiki-Operating-Rules.md`를 업데이트한다.
- 사람용 요청 예시, 사용 흐름, LLM 호출 가이드가 바뀌면 `wiki/Home/Wiki-Usage-Guide.md`를 업데이트한다.
- 둘 다 영향이 있으면 같은 브랜치와 같은 PR 범위에서 함께 수정한다.
- `AGENTS.md` 계열과 사용자 문서가 충돌하면 `AGENTS.md` 계열을 기준 진실로 보고, 같은 브랜치와 같은 PR 범위에서 사용자 문서를 함께 정정한다.
- 변경된 규칙이 사용자 요청 문장, 승인 흐름, 작업 순서 예시에 영향을 주면 `wiki/Home/Wiki-Usage-Guide.md`에 예시 요청을 최소 1개 함께 추가한다.
- 영향이 없어 사용자 문서 수정을 생략하면 변경 요약 또는 PR 본문 `비고`에 생략 사유를 짧게 남긴다.

## 규칙 변경 PR 체크 항목
- PR이 같은 저장소의 이슈를 완전히 해결하면 `비고`에 `Closes #<번호>`를 적는다.
- 관련은 있지만 완전히 닫지 않으면 `Closes` 대신 `Refs #<번호>`를 적는다.
- wiki 규칙/가이드/운영 문서 수정 PR의 `비고`에는 `사용자 문서 동기화 여부`, `issue/template 변경 여부`, `생략 사유`를 짧게 적는다.
- `Wiki-Usage-Guide.md`에 예시 요청을 추가했다면 어떤 예시를 추가했는지 `비고`에 함께 적는다.
- 사용자 문서 수정이나 template 변경이 없으면 `없음`과 사유를 분명히 적는다.

## PR 제목 규칙
- wiki 규칙/가이드/운영 문서 수정 PR이면 제목을 `docs: <주제>`로 쓴다.
- 프로젝트 PR 반영 PR이면 제목을 `pr: <project-pr-number> <주제>`로 쓴다.
- `<주제>`는 한글 짧은 명사구로 적고, 브랜치 prefix나 PR 번호를 제목 본문에서 중복 반복하지 않는다.

## PR 본문 템플릿
- 연결할 같은 저장소 이슈가 있으면 `비고`에 `Closes #<번호>` 또는 `Refs #<번호>`를 함께 적는다.
- `docs` PR 본문은 아래 순서를 고정한다.

```md
## 변경 요약
- ...

## 반영 문서
- ...

## 비고
- ...
```

- `pr` PR 본문은 아래 순서를 고정한다.

```md
## 기준 작업
- 프로젝트 PR: #<번호>
- 기준 branch/commit: <branch>@<commit>

## 변경 요약
- ...

## 반영 문서
- ...

## 비고
- ...
```

- `반영 문서`에는 실제로 수정한 wiki 문서만 적는다.
- `비고`에는 남은 작업, 의도적으로 제외한 범위, 리뷰 포인트만 짧게 적는다.

## LLM 작성 순서
1. 대상 프로젝트 `repo / branch / commit`과 wiki 기준 `origin/main@<hash>`를 확인한다.
2. 프로젝트 저장소 `execution_path`와 현재 실행 컨텍스트를 확인한다.
3. 커밋된 문서는 가능하면 `git show <ref>:<path>`로 읽는다.
4. `wiki/index.md`, `wiki/Home/README.md`, `wiki/03-Status/Current-State.md`, `wiki/03-Status/Next-Work.md`를 확인한다.
5. `wiki/05-Sources/`를 갱신한다.
6. 필요 시 `wiki/02-Architecture/`를 갱신한다.
7. 필요 시 `wiki/03-Status/`를 갱신한다.
8. 필요 시 `wiki/04-Records/`를 갱신한다.
9. 필요 시 `wiki/index.md`를 갱신한다.
10. 의미 있는 업데이트 단위면 `wiki/log.md`를 기록한다.

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

## LLM publish 절차
1. 프로젝트 브랜치 PR 완료 또는 현재 완료 작업 기준이 정리된 상태에서 사용자 wiki 등록 요청을 확인한다. `지금 완료된 작업 wiki에 등록해줘.` 같은 짧은 요청도 여기에 포함한다.
2. `git fetch origin main`으로 wiki 기준 `origin/main@<hash>`를 다시 확인한다.
3. wiki 반영 브랜치는 wiki 저장소에서 생성한다. 프로젝트 저장소에서 같은 이름의 wiki 반영 브랜치를 만들지 않는다.
   - 기본 형식: `docs/<topic-slug>`
   - 프로젝트 PR 연계 형식: `pr/<project-pr-number>-<topic-slug>`
4. `<topic-slug>`는 위 slug 규칙을 따른다.
5. 프로젝트 PR 반영이면 위 체크리스트 기준으로 wiki 문서를 갱신한다.
6. 변경 요약, `PR` 제목/본문, 관련 `issue` 초안이 필요하면 위 언어 규칙과 `PR 제목 규칙` / `PR 본문 템플릿`에 따라 한글로 정리한다.
   - PowerShell에서는 한글 본문을 stdin으로 넘기지 않고 UTF-8 파일 기반으로 작성한다.
7. 변경 요약을 제시하고 사용자 동의를 받은 뒤 커밋한다.
8. PR용 요약을 정리하고 사용자 동의를 받은 뒤 push / PR을 진행한다.
9. wiki `main` 머지도 사용자 동의와 검토를 전제로 진행한다.

## Current-State 와 Next-Work 차이
- `Current-State`
  - 지금 기준 커밋에서 이미 사실인 상태를 적는다.
  - 완료 / 부분 완료 / 미정리 영역을 적는다.
- `Next-Work`
  - Current-State를 읽은 뒤 다음에 해야 할 작업을 적는다.
  - 우선순위, 이유, 근거, 상태를 적는다.

## index / log 사용 기준
- 새 문서를 만들거나 삭제하면 `index.md`를 반드시 갱신한다.
- 기존 문서의 제목, 경로, 카탈로그 요약이 바뀌어도 `index.md`를 갱신한다.
- 기존 문서 본문만 보강한 경우 `index.md`는 생략 가능하다.
- `log.md`는 ingest / backfill / 구조 변경 / 상태 변경 / 규칙 변경처럼 의미 있는 업데이트 단위만 기록한다.
- 오탈자 수정, 표현 정리, 문장 다듬기처럼 의미 변화가 없는 자잘한 수정은 기록하지 않는다.
