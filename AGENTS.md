# AGENTS.md

## 목적
- 이 저장소는 프로젝트와 분리된 wiki 저장소다.
- 이 파일은 wiki 저장소 루트에서 세션이 시작될 때 적용할 전역 규칙과 진입 규칙만 다룬다.
- 프로젝트 쪽 요청 해석 규칙의 기준 진실은 프로젝트 저장소의 `AGENTS.md`에 둔다.
- wiki 내부 읽기/쓰기/반영 절차의 상세 규칙은 `wiki/AGENTS.md`에서 관리한다.

## 적용 범위
- 이 파일은 wiki 저장소 루트 진입 규칙 초안이다.
- 프로젝트 세션의 bootstrap, `wiki` 요청 해석, 프로젝트 기준 commit 해석은 여기서 다시 정의하지 않는다.
- 이 저장소에 직접 들어와 작업할 때 필요한 구조, 기준 commit, 읽기 기본값, 역할 분리만 정의한다.

## 문서 역할 분리
- `/AGENTS.md`
  - 저장소 루트 진입 규칙과 전역 기본값
- `/wiki/AGENTS.md`
  - `wiki/` 내부 작업 상세 규칙
- `/wiki/Home/README.md`
  - wiki 진입점
- `/wiki/Home/Wiki-Operating-Rules.md`
  - 팀 공유용 운영 설명서
- `/wiki/Home/Wiki-Usage-Guide.md`
  - 사람용 요청 예시 문서
  - 실행 규칙의 원본이 아니라 사용 예시를 제공하는 문서

## 저장소 구조
```text
raw/      # 원본 또는 원본 참조 정보
wiki/     # 공식 문서
Output/   # 세션 결과, 임시 분석, 보고 초안
```

## 기준 진실 우선순위
```text
code@commit
> merged PR
> open PR
> issue
> output/session
```

## 기준 커밋 원칙
- wiki는 항상 특정 `branch + commit` 기준으로 읽고 쓴다.
- 문서 해석 기준은 현재 워킹트리가 아니라 확정된 커밋 상태다.
- 미커밋 변경은 baseline에 포함하지 않는다.
- 같은 질문은 같은 `commit` 기준이면 같은 답이 나와야 한다.
- 사용자의 각 요청이나 중요한 판단 단계 전에 `git fetch origin main`으로 원격 최신 상태를 다시 확인하고 `origin/main@<hash>`를 기준 ref로 확정한다.
- `git fetch`가 성공하면 읽기와 판단은 원칙적으로 `origin/main@<hash>` 기준으로 수행한다.
- `git fetch`가 실패하면 최신이라고 단정하지 않고, 실패 사유와 마지막으로 확인 가능한 기준 `branch + commit`을 먼저 알린다.

## 문서 원문 읽기 기본값
- 커밋된 문서는 원칙적으로 `git show <ref>:<repo-relative-path>`로 먼저 읽는다.
- 기준 `ref`가 불명확하면 먼저 이번 판단의 `branch + commit`을 확정한 뒤 읽는다.
- `Get-Content`, `Select-String`, 기타 파일 시스템 읽기는 미커밋 변경, 신규 파일, 워킹트리 상태 확인처럼 fallback 사유가 있을 때만 사용한다.
- fallback 파일 읽기가 필요하면 UTF-8을 명시한 방식만 사용한다.
- 같은 턴에서 이미 `git show`로 확인한 커밋 문서를 파일 시스템 읽기로 다시 중복 확인하지 않는다.

## 프로젝트 세션과의 역할 분리
- 프로젝트 세션에서 들어오는 `wiki` 요청의 해석 기준은 프로젝트 저장소의 `AGENTS.md`를 따른다.
- 이 저장소는 연결된 wiki 저장소로 확정된 뒤의 읽기, 문서 수정, 반영 브랜치, commit, PR 절차를 담당한다.
- 프로젝트 저장소의 `./.local/wiki-repo.yml` 같은 bootstrap 로컬 설정은 이 저장소에서 관리하지 않는다.
- 현재 저장소 내부의 규칙으로 프로젝트 세션 bootstrap 규칙을 다시 정의하지 않는다.

## 읽기 시작 규칙
- 사용자가 `wiki 읽고 내용 확인해`, `wiki 보고 정리해`, `wiki 기준으로 말해줘`라고 요청하면 아래 순서로 먼저 읽는다.
  1. `git fetch origin main`으로 원격 최신 상태를 확인하고 이번 답변의 기준 `origin/main@<hash>`를 확정한다.
  2. 커밋된 원문은 원칙적으로 `git show <ref>:<path>`로 읽는다.
  3. `wiki/index.md`
  4. `wiki/Home/README.md`
  5. `wiki/03-Status/Current-State.md`
  6. `wiki/03-Status/Next-Work.md`
- 그 다음 세부 규칙은 `wiki/AGENTS.md`를 따른다.

## 직접 진입 시 주의점
- 이 저장소에 직접 들어와 작업할 때는 프로젝트 쪽 요청 의도가 이미 정해졌다고 가정하지 않는다.
- 프로젝트 기준 PR, commit, 반영 범위가 명확하지 않으면 최소 질문으로 기준을 확인한다.
- 프로젝트 세션에서 이미 `저장소 최신 여부 확인`인지 `문서 반영 점검`인지 해석이 끝난 경우에는 그 해석을 유지한다.

## 민감 정보 규칙
- 같이 쓰는 사람 전원이 봐도 되는 정보만 wiki에 올린다.
- 비밀번호, 토큰, API key, `.env` 값, 개인 연락처, 계정 식별자, 내부 URL/IP, 운영 DB 값은 올리지 않는다.
- 애매하면 민감 정보로 간주한다.
- 필요 시 `[REDACTED]`로 표시한다.
