# AGENTS.md

## 목적
- `raw/issues`는 GitHub issue 원본 참조 정보를 최소 단위로 기록하는 계층이다.

## 운영 규칙
- issue 본문 전체를 raw에 복사하지 않는다.
- raw issue는 `링크 + 최소 메타데이터`만 유지한다.
- GitHub issue 템플릿은 코드 repo의 `.github/ISSUE_TEMPLATE/*.md`를 기준으로 확인한다.
- issue는 **왜/무엇**의 원본으로 본다.
  - 어떤 문제/요구가 있었는지
  - 왜 이 작업이 필요한지
  - 기대 결과와 배경이 무엇인지
- 구현 상세, 원인 분석, 설계 판단은 wiki 문서에서 다룬다.
- issue 상세 카드에는 아래 정보를 최소한으로 적는다.
  - issue 번호
  - 제목
  - URL
  - 상태
  - 관련 PR
  - 관련 commit
  - 캡처 날짜
- 해석과 원인 분석은 `wiki/04-Records/Issues/` 또는 `wiki/05-Sources/issues/`에서 다룬다.

## 미래 issue 운영 규칙
- 앞으로 생성되는 issue는 모두 `raw/issues`에 먼저 기록한다.
- 현재 상태나 다음 작업에 영향을 주는 issue면 `wiki/03-Status/Current-State.md`, `wiki/03-Status/Next-Work.md`를 함께 갱신한다.
- 상세 source나 records 승격은 재사용 가치가 있을 때만 수행한다.
