## 목적
- `wiki/`는 Votedots 프로젝트의 **공식 문서와 산출물**을 관리하는 계층이다.
- LLM은 `wiki/`를 읽고 아래를 빠르게 답할 수 있어야 한다.
  - 프로젝트가 무엇인지
  - 지금 어디까지 됐는지
  - 다음에 무엇을 해야 하는지
  - 왜 그렇게 작업/결정했는지

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

## LLM 기본 읽기 순서
- 사용자가 `wiki 읽고 내용 확인해`, `wiki 보고 정리해`, `wiki 기준으로 말해줘`라고 하면 아래 순서로 먼저 읽는다.
  1. `wiki/index.md`
  2. `wiki/Home/README.md`
  3. `wiki/03-Status/Current-State.md`
  4. `wiki/03-Status/Next-Work.md`
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

## LLM 작성 순서
1. 대상 `branch + commit` 확인
2. `wiki/index.md`, `wiki/Home/README.md`, `wiki/03-Status/Current-State.md`, `wiki/03-Status/Next-Work.md` 확인
3. `wiki/05-Sources/` 갱신
4. 필요 시 `wiki/02-Architecture/` 갱신
5. 필요 시 `wiki/03-Status/` 갱신
6. 필요 시 `wiki/04-Records/` 갱신
7. 필요 시 `wiki/index.md` 갱신
8. 의미 있는 업데이트 단위면 `wiki/log.md` 기록

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
