# AGENTS.md

## 목적
- `raw/repos`는 프로젝트 repo를 어떤 기준으로 읽고 ingest했는지 기록하는 참조 계층이다.
- 공용 repo 정보와 사용자별 로컬 경로 정보를 분리해서 관리한다.

## 파일 역할
- `_repo-source-card.template.md`: 공용 raw repo 카드 템플릿
- `_repo-local-card.template.md`: 개인 실행 경로 카드 템플릿
- `{repo}.md`: 공용 카드. remote URL, branch, commit, ingest 범위만 기록
- `{repo}.local.md`: 개인 로컬 카드. `execution_path` 같은 실행 경로 메타데이터를 기록하고 git에 올리지 않음

## 규칙
- repo 원본은 읽기 전용으로만 다룬다.
- 공용 카드에는 사용자별 실행 경로를 적지 않는다.
- 실제 실행 경로가 필요하면 `{repo}.local.md`를 먼저 확인한다.
- 프로젝트 세션의 wiki repo 경로 1차 기준은 프로젝트 저장소의 `./.local/wiki-repo.yml`이다.
- `{repo}.local.md`는 프로젝트 세션의 wiki 경로 bootstrap 파일로 쓰지 않는다.
- `{repo}.local.md`에는 `execution_path`처럼 개인 실행 환경에서만 필요한 값만 적는다.
- ingest 결과 해석은 `wiki/05-Sources/`와 상태 문서에 기록한다.
- 경로, 링크, 메타데이터 외의 해석은 `raw/repos`에 적지 않는다.
