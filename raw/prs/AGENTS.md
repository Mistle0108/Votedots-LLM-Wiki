# AGENTS.md

## 목적
- `raw/prs`는 GitHub PR 원본 참조 정보를 최소 단위로 기록하는 계층이다.

## 운영 규칙
- PR 본문 diff 전체를 raw에 복사하지 않는다.
- raw PR은 `링크 + 최소 메타데이터 + 기준 commit`만 유지한다.
- GitHub PR 템플릿은 코드 repo의 `.github/pull-request-template.md`를 기준으로 확인한다.
- PR은 **어떻게/무엇이 바뀌었는지**의 원본으로 본다.
  - 어떤 코드가 바뀌었는지
  - 어떤 파일/모듈이 수정됐는지
  - 어떤 방식으로 해결했는지
- 구현 판단, 설계 이유, 우선순위 해석은 wiki 문서에서 다룬다.
- PR 상세 카드에는 아래 정보를 최소한으로 적는다.
  - PR 번호
  - 제목
  - URL
  - 기준 branch
  - merge commit
  - merge 날짜
  - 관련 issue
  - 관련 worklog / decision
- 해석과 판단 근거는 `wiki/04-Records/Decisions/` 또는 `wiki/05-Sources/prs/`에서 다룬다.

## 미래 PR 운영 규칙
- 앞으로 merge되는 PR은 모두 `raw/prs`에 먼저 기록한다.
- 현재 상태나 다음 작업에 영향을 주는 PR이면 `wiki/03-Status/Current-State.md`, `wiki/03-Status/Next-Work.md`를 함께 갱신한다.
- 상세 source나 records 승격은 재사용 가치가 있을 때만 수행한다.
