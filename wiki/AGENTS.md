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
- 사용자의 명령을 wiki 기준으로 수행하기 전에는 먼저 wiki 로컬 저장소와 원격 `origin/main`이 같은지 확인한다.
- 가능하면 `git fetch origin main` 후 로컬 `main`과 `origin/main`을 비교한다.
- 원격 확인이 불가능하거나 로컬/원격이 다르면, 최신이라고 단정하지 말고 제한과 실제 사용 기준 `branch + commit`을 먼저 밝힌다.

## 문서 원문 읽기 기본값
- 커밋된 한글 Markdown 원문은 원칙적으로 `git show <ref>:<repo-relative-path>`로 먼저 읽는다.
- `<ref>`가 불명확하면 먼저 이번 판단의 기준 `branch + commit`을 확정한다.
- 이유: 현재 PowerShell 출력 인코딩 환경에서는 한글 문서가 깨질 수 있고, 처음부터 Git 객체를 읽는 편이 기준 commit 일관성과 토큰 사용 면에서도 더 효율적이다.
- `Get-Content`, `Select-String`, 기타 PowerShell 파일 읽기는 미커밋 변경, 신규 파일, 워킹트리 상태 확인이 필요할 때만 fallback으로 사용한다.
- 같은 턴에서 이미 `git show`로 읽은 커밋 문서를 PowerShell 파일 읽기로 다시 중복 확인하지 않는다.
- 필요한 경우에도 전체 파일 재읽기보다 필요한 섹션만 좁혀 읽는다.
- 커밋 기준 본문과 워킹트리 본문을 함께 읽었으면 둘을 섞어 말하지 말고 구분해서 설명한다.

## `git show` 사용 기준 표

| 상황 | 기본 확인 방식 | fallback | 메모 |
| --- | --- | --- | --- |
| 커밋된 한글 문서 원문 확인 | `git show <ref>:<path>` | 없음 | 먼저 기준 `branch + commit`을 확정한다. |
| 같은 커밋 문서의 특정 섹션 재확인 | `git show <ref>:<path>` 후 필요한 섹션만 확인 | 없음 | 같은 턴에서 PowerShell 파일 읽기로 다시 확인하지 않는다. |
| 미커밋 변경 확인 | `git diff -- <path>` | 파일 시스템 읽기 | baseline이 아니라 워킹트리 상태로 취급한다. |
| 신규 untracked 파일 확인 | 파일 시스템 읽기 | 없음 | Git 객체에 아직 없으므로 `git show` 대상이 아니다. |
| 워킹트리 전체 상태 확인 | `git status` | 파일 시스템 읽기 | 커밋 기준 내용과 섞지 말고 별도로 설명한다. |

## wiki 동기화 확인 절차
1. 기본 명령 순서는 `git fetch origin main` -> `git rev-parse main` -> `git rev-parse origin/main` 이다.
2. 두 해시가 같으면 `wiki local main == origin/main`으로 본다.
3. 두 해시가 같으면 `main@<hash>`를 이번 읽기/쓰기 기준으로 확정한다.
4. `git fetch`가 실패하거나 `main`이 없으면 최신이라고 단정하지 않고, 제한과 현재 사용 가능한 기준 `branch + commit`만 먼저 밝힌다.
5. 두 해시가 다르면 먼저 `wiki local main != origin/main` 사실과, 로컬 `main`을 `origin/main`에 `fast-forward`로 맞춘 뒤 계속 진행하겠다는 계획을 짧게 안내한다.
6. 현재 워킹트리 때문에 `main` 전환이 가능한지 확인한다. 미커밋 변경 때문에 전환이 안 되면 자동 정리하지 않고 실패 사유를 먼저 밝힌다.
7. 전환 가능하면 로컬 `main`으로 이동해 `git pull --ff-only origin main`으로 `origin/main`에 맞춘다.
8. `fast-forward`가 성공하면 `git rev-parse main`으로 새 기준 commit을 다시 확인하고, 그 commit을 이번 읽기/쓰기 기준으로 확정한다.
9. `fast-forward`가 실패하면 자동 `merge`, `rebase`, 강제 reset을 하지 않고 실패 사유를 먼저 밝힌다.
10. 긴 작업 중 새 사용자 명령이나 중요한 판단 직전에는 이 절차를 다시 수행한다.

## sync 불일치 대응 문구 예시
- 불일치 안내 예시:

```text
wiki 로컬 main과 origin/main이 다릅니다.
먼저 로컬 main을 origin/main에 fast-forward로 맞춘 뒤, 새 기준 commit으로 계속 진행하겠습니다.
```

- fast-forward 성공 예시:

```text
wiki local main을 origin/main@<commit>으로 fast-forward 했습니다.
이제 main@<commit> 기준으로 계속 진행합니다.
```

- fast-forward 실패 예시:

```text
wiki 로컬 main과 origin/main이 다르지만, 현재 상태에서는 main 전환 또는 fast-forward가 불가능합니다.
자동 merge/rebase는 하지 않고, 실패 사유와 현재 기준 상태를 먼저 공유합니다.
```

## 프로젝트 세션 연계 규칙
- 프로젝트 작업을 위해 wiki를 읽거나 wiki 등록을 준비할 때는 프로젝트 저장소의 `execution_path` 기준 세션에서 진행한다.
- 프로젝트 세션에서는 로컬 wiki를 참조 문서로 읽고, 각 사용자 명령과 중요한 판단 단계 전에 wiki 로컬/원격 일치 여부를 다시 확인한다.
- 프로젝트 저장소 경로가 필요하면 `raw/repos/{repo}.local.md`의 `execution_path`를 먼저 확인하고, 없으면 세션 입력으로 받는다.
- 프로젝트 코드 확인, 설계, 구현, 검증은 프로젝트 저장소에서 수행하고, wiki 저장소는 문서 반영 브랜치와 공유 문서 관리 용도로만 사용한다.
- wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 모두 wiki 저장소에서 수행한다. 프로젝트 저장소에서는 반영 범위만 정리하고, 실제 git 작업은 wiki 저장소 기준으로 진행한다.
- 프로젝트 브랜치 PR이 완료된 뒤 사용자가 wiki 등록을 요청하면, 먼저 프로젝트 PR/merge commit 기준으로 반영 범위를 정리한다.

## LLM 기본 읽기 순서
- 사용자가 `wiki 읽고 내용 확인해`, `wiki 보고 정리해`, `wiki 기준으로 말해줘`라고 하면 아래 순서로 먼저 읽는다.
  1. wiki 로컬 `main`과 `origin/main`의 최신 상태가 같은지 확인하고, 이번 답변의 기준 `branch + commit`을 확정한다.
  2. 프로젝트 연계 질문이면 프로젝트 저장소 `execution_path`와 현재 실행 컨텍스트를 확인한다.
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

## LLM 응답 원칙
- wiki를 읽기 전에 기억만으로 답하지 않는다.
- wiki에 없는 내용은 추측하지 않는다.
- wiki로 답하기 부족하면 어떤 문서가 부족한지 먼저 말한다.
- 필요할 때만 `raw/`를 마지막 수단으로 읽는다.
- wiki 로컬/원격 최신 상태를 확인하지 못했으면 최신 기준이라고 단정하지 않는다.
- wiki를 근거로 현재 상태나 다음 작업을 말할 때는 기준 `branch + commit` 또는 확인 실패 사유를 먼저 밝힌다.
- 커밋 기준 본문과 워킹트리 본문을 함께 썼으면 어떤 부분이 어느 기준인지 구분해서 설명한다.
- 사람용 안내 문서와 LLM 규칙 문서가 동시에 보이면, LLM은 항상 `AGENTS.md` 계열 규칙을 우선한다.
- 커밋된 한글 문서 원문 확인은 처음부터 Git 객체 기준으로 수행하고, fallback 사유가 없으면 PowerShell 파일 읽기로 우회하지 않는다.
- sync 불일치가 있으면 `불일치 안내 -> fast-forward 시도/실패 결과 -> 새 기준 commit 또는 실패 사유` 순서로 짧게 설명한다.

## 이슈 / PR 작성 언어
- 새로 작성하는 GitHub `issue` 제목/본문, `PR` 제목/본문, 변경 요약은 기본적으로 한글로 작성한다.
- 다른 언어는 사용자가 명시적으로 요청한 경우에만 사용한다.
- 원문 메타데이터나 외부 원문 인용은 source 기준을 유지하되, 새로 작성하는 설명과 요약은 한글을 기본으로 한다.

## PR 제목 규칙
- wiki 규칙/가이드/운영 문서 수정 PR이면 제목을 `docs: <주제>`로 쓴다.
- 프로젝트 PR 반영 PR이면 제목을 `pr: <project-pr-number> <주제>`로 쓴다.
- `<주제>`는 한글 짧은 명사구로 적고, 브랜치 prefix나 PR 번호를 제목 본문에서 중복 반복하지 않는다.

## PR 본문 템플릿
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
1. 대상 프로젝트 `repo / branch / commit`과 wiki 로컬/원격 최신 상태를 확인한다.
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
1. 프로젝트 브랜치 PR 완료와 사용자 wiki 등록 요청을 확인한다.
2. wiki 로컬 `main`과 `origin/main`이 같은지 다시 확인한다.
3. wiki 반영 브랜치는 wiki 저장소에서 생성한다. 프로젝트 저장소에서 같은 이름의 wiki 반영 브랜치를 만들지 않는다.
   - 기본 형식: `docs/<topic-slug>`
   - 프로젝트 PR 연계 형식: `pr/<project-pr-number>-<topic-slug>`
4. `<topic-slug>`는 위 slug 규칙을 따른다.
5. 프로젝트 PR 반영이면 위 체크리스트 기준으로 wiki 문서를 갱신한다.
6. 변경 요약, `PR` 제목/본문, 관련 `issue` 초안이 필요하면 위 언어 규칙과 `PR 제목 규칙` / `PR 본문 템플릿`에 따라 한글로 정리한다.
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
