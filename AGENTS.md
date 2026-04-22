# AGENTS.md

## 목적
- 이 저장소는 Votedots 프로젝트의 별도 wiki repo다.
- 목적은 wiki를 통해 아래 3가지를 빠르게 파악하게 하는 것이다.
  - 지금 어디까지 됐는가
  - 다음에 무엇을 해야 하는가
  - 왜 그렇게 작업/결정했는가

## 저장소 구조
```text
raw/      # 원본 또는 원본 참조 정보
wiki/     # 공식 문서
Output/   # 세션 결과, 임시 분석, 보고 초안
```

## 문서 역할 분리
- `/AGENTS.md`
  - LLM 전역 행동 규칙
- `/wiki/AGENTS.md`
  - `wiki/` 내부 작업 규칙
- `/wiki/Home/README.md`
  - wiki 진입점
- `/wiki/Home/Wiki-Operating-Rules.md`
  - 팀 공유용 운영 설명서
- `/README.md`
  - 저장소 첫 화면 안내

## 기준 진실 우선순위
```text
code@commit      # 특정 branch + commit에서 실제로 확인한 코드
> merged PR      # 이미 병합된 변경 이력
> open PR        # 아직 병합되지 않은 제안 변경
> issue          # 요구사항, 문제, 배경
> output/session # 세션 메모, 임시 분석, 임시 결과물
```

## 기준 커밋 원칙
- wiki는 항상 특정 `branch + commit` 기준으로 작성한다.
- 기준 진실은 항상 `code@commit`이다.
- 문서 해석 기준은 현재 워킹트리가 아니라 확정된 커밋 상태다.
- 미커밋 변경은 baseline에 포함하지 않는다.
- 같은 질문은 같은 `commit` 기준이면 같은 답이 나와야 한다.

## raw 운영 규칙
- 초기 raw 범위는 `repo + issues + PR`이다.
- `raw/`는 원본 또는 원본 참조 계층이다.
- `raw/`에는 해석, 판단, 우선순위를 적지 않는다.
- repo는 읽기 전용으로 참조하고 ingest 기준 `commit hash`를 기록한다.
- `raw/issues`는 GitHub issue 원문 메타데이터 기준이다.
- `raw/prs`는 GitHub PR 메타데이터 + merge commit 기준이다.
- 사용자별 `execution_path`는 shared repo에 커밋하지 않는다.
- 실제 실행 경로는 gitignored `raw/repos/{repo}.local.md` 또는 세션 입력으로만 받는다.

## wiki 작성 원칙
- 같은 역할의 문서는 새로 만들기보다 기존 문서를 먼저 갱신한다.
- `05-Sources`에는 사실만 적고, 해석은 `01-Project`, `02-Architecture`, `03-Status`, `04-Records`에 적는다.
- 모든 공식 wiki 문서는 YAML frontmatter를 포함한다.
- 단, `AGENTS.md` 계열 운영 규칙 파일은 예외로 한다.
- 이유: `AGENTS.md`는 산출물 페이지가 아니라 LLM 행동 규칙 파일이므로, 규칙 본문 자체가 더 중요하다.
- wiki 내부 링크는 wikilink만 사용한다.

## frontmatter 최소 규칙
모든 공식 wiki 문서:

```yaml
---
title:
type:
status:
updated:
tags:
---
```

소스 문서 추가 필드:

```yaml
source_kind:
source_ref:
commit:
```

## index / log 규칙
- `wiki/index.md`
  - 새 문서를 만들거나 삭제하면 반드시 갱신한다.
  - 기존 문서의 제목, 경로, 문서 역할, 카탈로그 요약이 바뀌면 갱신한다.
  - 기존 문서의 본문만 보강한 경우에는 생략 가능하다.
- `wiki/log.md`
  - ingest / backfill / 구조 변경 / 상태 변경 / 규칙 변경처럼 의미 있는 업데이트 단위만 기록한다.
  - 오탈자 수정, 표현 다듬기, 문장 순서 조정처럼 의미 변화가 없는 자잘한 수정은 기록하지 않는다.
  - 같은 주제의 작은 수정은 한 번의 로그 엔트리로 묶는다.

## 읽기 시작 규칙
- 사용자가 `wiki 읽고 내용 확인해`, `wiki 보고 정리해`, `wiki 기준으로 말해줘`라고 요청하면 아래 순서로 먼저 읽는다.
  1. `wiki/index.md`
  2. `wiki/Home/README.md`
  3. `wiki/03-Status/Current-State.md`
  4. `wiki/03-Status/Next-Work.md`
- 그 다음 세부 규칙은 `wiki/AGENTS.md`를 따른다.

## 갱신 원칙
- 앞으로 생기는 issue / PR은 먼저 `raw/`에 기록한다.
- 현재 상태를 바꾸는 작업이면 `wiki/03-Status/Current-State.md`를 갱신한다.
- 다음 작업 우선순위를 바꾸는 작업이면 `wiki/03-Status/Next-Work.md`를 갱신한다.
- `05-Sources`와 `04-Records`는 재사용 가치가 있을 때만 선별 승격한다.

## publish 규칙
- wiki 반영은 direct push가 아니라 `branch + PR` 기준으로 운영한다.
- 기준 커밋을 바탕으로 wiki 내용을 먼저 작성 / 갱신한다.
- 변경 내용을 짧게 요약한 뒤 `커밋할까?`라고 사용자 동의를 받는다.
- 동의가 있을 때만 로컬 커밋을 진행한다.
- 커밋 후 PR용 변경 요약을 정리한 뒤 `PR 요청할까?`라고 다시 동의를 받는다.
- 동의가 있을 때만 push / PR 생성을 진행한다.

## 민감 정보 규칙
- 같이 쓰는 사람 전원이 봐도 되는 정보만 wiki에 올린다.
- 비밀번호, 토큰, API key, `.env` 값, 개인 연락처, 계정 식별자, 내부 URL/IP, 운영 DB 값은 올리지 않는다.
- 애매하면 민감 정보로 간주한다.
- 필요 시 `[REDACTED]`로 표시한다.
