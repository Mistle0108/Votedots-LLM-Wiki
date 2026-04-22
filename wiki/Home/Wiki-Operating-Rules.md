---
title: Wiki Operating Rules
type: wiki-operating-rules
status: active
updated: 2026-04-22
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
  - 루트 `AGENTS.md`는 저장소 전역 규칙, 진입 순서, 읽기 기본값을 다룬다.
  - `wiki/AGENTS.md`는 wiki 문서 읽기/쓰기/publish의 상세 절차를 다룬다.
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
- 사용자의 명령을 wiki 기준으로 수행하기 전에는 먼저 wiki 로컬 저장소와 원격 `origin/main`의 최신 상태가 같은지 확인한다.
- 가능하면 `git fetch origin main` 후 로컬 `main`과 `origin/main`을 비교한다.
- 원격 확인이 불가능하거나 로컬/원격이 다르면 최신이라고 단정하지 말고, 제한과 실제 사용 기준 `branch + commit`을 먼저 밝힌다.

## wiki 동기화 확인 절차
1. 기본 명령 순서는 `git fetch origin main` -> `git rev-parse main` -> `git rev-parse origin/main` 이다.
2. 두 해시가 같으면 `wiki local main == origin/main`으로 본다.
3. 두 해시가 같으면 `main@<hash>`를 이번 읽기/쓰기 기준으로 확정한다.
4. `git fetch` 실패, `main` 부재, 두 해시 불일치면 최신이라고 단정하지 않는다.
5. 이 경우 자동 `pull`, `merge`, `rebase`를 하지 않고, 제한과 현재 사용 가능한 기준 `branch + commit`만 먼저 밝힌다.
6. 긴 작업 중 새 요청 시작 전이나 중요한 판단 직전에는 이 절차를 다시 수행한다.

## 문서 원문 읽기 기본값
- 커밋된 한글 Markdown 원문은 기본적으로 파일 시스템 직접 읽기보다 Git 객체 경로 읽기를 우선한다.
- 기본 형식은 `git show <ref>:<repo-relative-path>`다.
- `<ref>`가 불명확하면 먼저 이번 판단의 기준 `branch + commit`을 확정한다.
- 이유: 현재 PowerShell 출력 인코딩 환경에서는 한글 문서가 깨질 수 있으므로, 커밋된 원문은 Git 객체에서 직접 읽는 편이 더 안정적이다.
- 미커밋 변경, 신규 파일, 워킹트리 상태 확인이 필요하면 파일 시스템 읽기, `git diff`, `git status`를 fallback으로 사용한다.
- 커밋 기준 본문과 워킹트리 본문을 함께 사용했으면 둘을 구분해서 설명한다.

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
- 이 파일에는 `execution_path`만 기록한다.
- `{repo}.local.md`는 gitignored 파일이므로 원격 저장소에 올라가지 않는다.
- LLM이 repo ingest를 수행할 때는 먼저 이 파일을 확인하고, 없으면 세션 입력으로 경로를 받는다.

## 프로젝트 세션 연계 규칙
- 기본 작업 컨텍스트는 프로젝트 저장소 세션이다.
- 사용자는 프로젝트 세션에서 로컬 wiki를 읽고 현재 상태, 다음 작업, 근거 문서를 확인한다.
- 프로젝트 코드 확인, 구현, 검증은 프로젝트 저장소에서 수행하고, wiki 저장소는 문서 반영 브랜치와 공유 문서 관리 용도로만 사용한다.
- wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 모두 wiki 저장소에서 수행한다. 프로젝트 저장소에서는 반영 범위만 정리하고 실제 git 작업은 하지 않는다.
- 프로젝트 세션에서 여러 요청을 이어 처리할 때도, 새 요청 시작 전과 중요한 판단 단계 전에는 wiki 로컬/원격 일치 여부를 다시 확인한다.
- 프로젝트 작업이 끝나고 브랜치 PR이 완료되면, 사용자는 같은 프로젝트 세션에서 현재 완료된 작업에 대한 wiki 등록을 요청한다.

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

## 이슈 / PR 작성 언어
- 새로 작성하는 GitHub `issue` 제목/본문, `PR` 제목/본문, 변경 요약은 기본적으로 한글로 작성한다.
- 다른 언어는 사용자가 명시적으로 요청한 경우에만 사용한다.
- 원문 메타데이터나 외부 원문 인용은 source 기준을 유지하되, 새로 작성하는 설명과 요약은 한글을 기본으로 한다.

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
1. wiki 로컬 `main`과 `origin/main` 최신 상태를 확인
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
  1. wiki 로컬 `main`과 `origin/main` 최신 상태를 확인한다.
  2. `wiki/index.md`
  3. `wiki/Home/README.md`
  4. `wiki/03-Status/Current-State.md`
  5. `wiki/03-Status/Next-Work.md`
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

## publish 규칙
1. 프로젝트 브랜치 PR이 완료되고 사용자가 wiki 등록을 요청하면, 같은 프로젝트 세션에서 기준 프로젝트 PR/merge commit과 반영 범위를 먼저 정리한다.
2. wiki 반영 직전에는 wiki 로컬 `main`과 `origin/main`이 같은지 다시 확인한다.
3. wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 모두 wiki 저장소에서 수행한다. 프로젝트 저장소에서 wiki 반영 브랜치를 만들지 않는다.
4. wiki 반영은 direct push가 아니라 `branch + PR` 기준으로 운영한다.
5. wiki 반영 브랜치는 기본적으로 `docs/<topic-slug>`를 사용한다.
6. 특정 프로젝트 PR에 대응하는 반영이면 `pr/<project-pr-number>-<topic-slug>` 형식을 사용한다.
7. `<topic-slug>`는 위 slug 규칙을 따른다.
8. 프로젝트 PR 반영이면 위 체크리스트 기준으로 wiki 내용을 먼저 작성 / 갱신한다.
9. 변경 내용 요약, `PR` 제목/본문, 관련 `issue` 초안이 필요하면 위 언어 규칙에 따라 한글로 정리한다.
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
- wiki는 항상 `code@commit` 기준으로 읽고 쓰며, 사용 전에는 로컬 `main`과 `origin/main` 일치 여부를 확인한다.
