# AGENTS.md

## 목적
- 이 저장소는 Votedots 프로젝트의 별도 wiki repo다.
- 루트 `AGENTS.md`는 저장소 전역 규칙과 진입 규칙만 다룬다.
- wiki 내부 읽기/쓰기/반영 절차의 상세 규칙은 `wiki/AGENTS.md`에서 관리한다.

## 왜 둘 다 필요한가
- `/AGENTS.md`
  - 저장소 루트에서 세션이 시작될 때 바로 적용되는 전역 규칙
  - 저장소 구조, 기준 진실, 읽기 기본값, 민감 정보 규칙, 진입 순서 정의
- `/wiki/AGENTS.md`
  - `wiki/` 내부 작업 전용 상세 규칙
  - 문서 역할, 읽기 순서, 상태/기록/소스 갱신 기준, publish 절차 정의
- 즉, 둘 다 필요하지만 역할은 달라야 한다.
- 상세한 wiki 작업 규칙은 `wiki/AGENTS.md`에 두고, 루트 `AGENTS.md`는 요약과 진입 규칙만 유지한다.

## 저장소 구조
```text
raw/      # 원본 또는 원본 참조 정보
wiki/     # 공식 문서
Output/   # 세션 결과, 임시 분석, 보고 초안
```

## 문서 역할 분리
- `/AGENTS.md`
  - 저장소 전역 행동 규칙
- `/wiki/AGENTS.md`
  - `wiki/` 내부 작업 상세 규칙
- `/wiki/Home/README.md`
  - wiki 진입점
- `/wiki/Home/Wiki-Operating-Rules.md`
  - 팀 공유용 운영 설명서
- `/wiki/Home/Wiki-Usage-Guide.md`
  - 프로젝트 세션 기준 사용 가이드
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
- wiki는 항상 특정 `branch + commit` 기준으로 읽고 쓴다.
- 기준 진실은 항상 `code@commit`이다.
- 문서 해석 기준은 현재 워킹트리가 아니라 확정된 커밋 상태다.
- 미커밋 변경은 baseline에 포함하지 않는다.
- 같은 질문은 같은 `commit` 기준이면 같은 답이 나와야 한다.
- 사용자의 명령을 wiki 기준으로 수행하기 전에는 먼저 wiki 로컬 저장소와 원격 `origin/main`의 최신 상태가 같은지 확인한다.
- 가능하면 `git fetch origin main` 후 로컬 `main`과 `origin/main`을 비교한다.
- 원격 확인이 불가능하거나 두 저장소가 일치하지 않으면, 최신이라고 단정하지 말고 제한과 실제 사용 기준 `branch + commit`을 먼저 밝힌다.

## 문서 원문 읽기 기본값
- 커밋된 한글 Markdown 원문은 기본적으로 파일 시스템 직접 읽기보다 Git 객체 경로 읽기를 우선한다.
- 기본 형식은 `git show <ref>:<repo-relative-path>`다.
- `<ref>`가 불명확하면 먼저 이번 판단의 기준 `branch + commit`을 확정한다.
- 이유: 현재 PowerShell 출력 인코딩 환경에서는 한글 문서가 깨질 수 있으므로, 커밋된 원문은 Git 객체에서 직접 읽는 편이 더 안정적이다.
- 미커밋 변경, 신규 파일, 워킹트리 상태 확인이 필요하면 파일 시스템 읽기, `git diff`, `git status`를 fallback으로 사용한다.
- 커밋 기준 본문과 워킹트리 본문을 함께 읽었으면 둘을 섞어 말하지 말고 구분해서 설명한다.

## raw 운영 규칙
- 초기 raw 범위는 `repo + issues + PR`이다.
- `raw/`는 원본 또는 원본 참조 계층이다.
- `raw/`에는 해석, 판단, 우선순위를 적지 않는다.
- repo는 읽기 전용으로 참조하고 ingest 기준 `commit hash`를 기록한다.
- `raw/issues`는 GitHub issue 원문 메타데이터 기준이다.
- `raw/prs`는 GitHub PR 메타데이터 + merge commit 기준이다.
- 사용자별 `execution_path`는 shared repo에 커밋하지 않는다.
- 실제 실행 경로는 gitignored `raw/repos/{repo}.local.md` 또는 세션 입력으로만 받는다.

## 프로젝트 세션 연계 규칙
- 프로젝트 작업을 위해 wiki를 읽거나 wiki 반영이 필요할 때는 프로젝트 저장소의 `execution_path` 기준 세션에서 진행한다.
- 프로젝트 세션에서는 로컬 wiki를 참조 문서로 읽고, 사용자의 각 명령이나 중요한 판단 단계 전에 wiki 로컬/원격 일치 여부를 다시 확인한다.
- 프로젝트 코드 확인, 설계, 구현, 검증은 프로젝트 저장소에서 수행하고, wiki 저장소는 문서화 대상과 반영 브랜치 용도로만 사용한다.
- wiki 반영 브랜치 생성, wiki 문서 commit, wiki PR 생성과 merge는 모두 wiki 저장소에서 진행한다. 프로젝트 저장소에서 wiki 반영 브랜치를 만들지 않는다.
- 프로젝트 브랜치 PR이 완료된 뒤 사용자가 wiki 등록을 요청하면, 같은 프로젝트 세션에서 먼저 반영 범위를 정리한다.
- 실제 wiki 반영 절차의 상세 순서는 `wiki/AGENTS.md`를 따른다.

## 읽기 시작 규칙
- 사용자가 `wiki 읽고 내용 확인해`, `wiki 보고 정리해`, `wiki 기준으로 말해줘`라고 요청하면 아래 순서로 먼저 읽는다.
  1. wiki 로컬 `main`과 `origin/main` 최신 상태가 같은지 확인한다.
  2. 가능하면 커밋된 원문은 `git show <ref>:<path>`로 읽는다.
  3. `wiki/index.md`
  4. `wiki/Home/README.md`
  5. `wiki/03-Status/Current-State.md`
  6. `wiki/03-Status/Next-Work.md`
- 그 다음 세부 규칙은 `wiki/AGENTS.md`를 따른다.

## publish 요약 규칙
- wiki 반영은 direct push가 아니라 `branch + PR` 기준으로 운영한다.
- 프로젝트 브랜치 PR이 완료되고 사용자가 wiki 등록을 요청하면, 프로젝트 세션에서 기준 프로젝트 PR/commit과 반영 범위를 먼저 정리한다.
- wiki 반영 직전에는 wiki 로컬 `main`과 `origin/main`이 같은지 다시 확인한다.
- 프로젝트 세션에서 반영 범위를 정리하더라도, 실제 wiki 반영 브랜치 생성과 git 작업 대상 저장소는 wiki 저장소다.
- 상세한 브랜치 규칙과 반영 절차는 `wiki/AGENTS.md`를 따른다.

## 민감 정보 규칙
- 같이 쓰는 사람 전원이 봐도 되는 정보만 wiki에 올린다.
- 비밀번호, 토큰, API key, `.env` 값, 개인 연락처, 계정 식별자, 내부 URL/IP, 운영 DB 값은 올리지 않는다.
- 애매하면 민감 정보로 간주한다.
- 필요 시 `[REDACTED]`로 표시한다.
