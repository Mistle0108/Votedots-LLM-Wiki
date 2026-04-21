---
title: Wiki Operating Rules
type: wiki-operating-rules
status: active
updated: 2026-04-21
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
  - LLM 전역 행동 규칙
- `/wiki/AGENTS.md`
  - `wiki/` 내부 작업 규칙
- `/wiki/Home/README.md`
  - wiki 진입점
- `/wiki/Home/Wiki-Operating-Rules.md`
  - 팀 공유용 운영 설명서

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
1. 대상 `repo / branch / commit hash` 확정
2. raw 참조 카드 갱신 또는 확인
3. 코드 / issue / PR 읽기
4. `05-Sources` 갱신
5. 필요 시 `02-Architecture` 갱신
6. 필요 시 `03-Status` 갱신
7. 필요 시 `04-Records` 갱신
8. 필요 시 `index.md` 갱신
9. 의미 있는 업데이트 단위면 `log.md` 기록

## LLM 기본 읽기 순서
- 사용자가 `wiki 읽고 내용 확인해`, `wiki 보고 정리해`, `wiki 기준으로 말해줘`라고 하면 아래 순서로 먼저 읽는다.
  1. `wiki/index.md`
  2. `wiki/Home/README.md`
  3. `wiki/03-Status/Current-State.md`
  4. `wiki/03-Status/Next-Work.md`
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
- 현재 상태를 바꾸는 작업이면 `03-Status/Current-State.md`를 항상 갱신한다.
- 다음 작업 우선순위를 바꾸는 작업이면 `03-Status/Next-Work.md`를 항상 갱신한다.
- `05-Sources`와 `04-Records`는 재사용 가치가 있을 때만 선별 승격한다.

## publish 규칙
1. 기준 커밋 기반으로 wiki 내용을 먼저 작성 / 갱신한다.
2. 변경 내용을 짧게 요약한다.
3. `커밋할까?`라고 사용자 동의를 받는다.
4. 동의가 있으면 로컬 커밋을 진행한다.
5. 커밋 후 PR용 변경 요약을 정리한다.
6. `PR 요청할까?`라고 사용자 동의를 받는다.
7. 동의가 있을 때만 push / PR 생성을 진행한다.
- `log.md` 기록과 git commit은 별개다.
- `log.md`는 의미 있는 wiki 변경을 남기고, git commit은 사용자 동의 후에만 진행한다.

## 한 줄 요약
- `05-Sources`에는 사실만 적는다.
- `03-Status`에는 현재 사실과 다음 행동을 적는다.
- `04-Records`에는 작업, 문제, 결정을 축적한다.
- wiki는 항상 `code@commit` 기준으로 읽고 쓴다.
