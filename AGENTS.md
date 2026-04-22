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
  - 프로젝트 세션 기준 사람용 사용 가이드
  - LLM 실행 규칙 원본이 아니라, 사용자가 LLM에게 어떻게 요청할지 보는 예시 문서
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
- 사용자의 명령을 wiki 기준으로 수행하기 전에는 wiki 로컬 `main`과 `origin/main` 일치 여부를 먼저 확인한다.
- 동기화 확인의 상세 명령과 실패 시 처리 원칙은 `wiki/AGENTS.md`를 따른다.
- 불일치가 확인되면 먼저 불일치 사실을 안내하고, 가능하면 로컬 `main`을 `origin/main`에 `fast-forward`로 맞춘 뒤 기준 commit을 다시 확정한다.
- `main` 전환이 안 되거나 `fast-forward`가 실패하면 자동 `merge`, `rebase`, 강제 reset은 하지 않고 실패 사유를 먼저 알린다.

## 문서 원문 읽기 기본값
- 커밋된 한글 문서는 원칙적으로 `git show <ref>:<repo-relative-path>`로 먼저 읽는다.
- 기준 `ref`가 불명확하면 먼저 이번 판단의 `branch + commit`을 확정한 뒤 읽는다.
- 한글 문서 확인에서 PowerShell 기본 출력 인코딩에 의존하지 않는다.
- `Get-Content`, `Select-String`, 기타 파일 시스템 읽기는 미커밋 변경, 신규 파일, 워킹트리 상태 확인처럼 fallback 사유가 있을 때만 사용한다.
- fallback 파일 읽기가 필요하면 `Get-Content -Encoding utf8`처럼 UTF-8을 명시한 방식만 사용한다.
- 출력 인코딩을 임시로 바꿔가며 여러 번 재시도하는 방식은 기본 경로로 쓰지 않는다.
- 같은 턴에서 이미 `git show`로 확인한 커밋 문서를 PowerShell 파일 읽기로 다시 중복 확인하지 않는다.
- 미커밋 변경, 신규 파일, 워킹트리 상태만 `git diff`, `git status`, 파일 시스템 읽기로 보완한다.
- 세부 fallback 규칙은 `wiki/AGENTS.md`를 따른다.

## raw 원칙
- `raw/`는 원본 또는 원본 참조 계층이다.
- 해석과 우선순위는 `wiki/` 문서에서 다루고, 상세 운영 규칙은 `wiki/AGENTS.md`를 따른다.

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
  2. 커밋된 원문은 원칙적으로 `git show <ref>:<path>`로 읽는다.
  3. `wiki/index.md`
  4. `wiki/Home/README.md`
  5. `wiki/03-Status/Current-State.md`
  6. `wiki/03-Status/Next-Work.md`
- 그 다음 세부 규칙은 `wiki/AGENTS.md`를 따른다.

## 사용법 안내 규칙
- 사용자가 `wiki를 어떻게 사용해?`, `wiki에서 뭐 물어볼 수 있어?`, `wiki에서 어떻게 확인해?`라고 물으면 `wiki/Home/Wiki-Usage-Guide.md` 기준의 세션용 요청 예시를 먼저 3~8개 제시한다.
- 문서 링크만 나열하지 말고, 사용자가 바로 복사해 쓸 수 있는 짧은 요청문을 우선 안내한다.
- 그 다음 필요할 때만 `Wiki Usage Guide`, `Home`, `Wiki Operating Rules` 순서로 관련 문서를 덧붙인다.

## publish 요약 규칙
- wiki 반영은 direct push가 아니라 `branch + PR` 기준으로 운영한다.
- 프로젝트 브랜치 PR이 완료되고 사용자가 wiki 등록을 요청하면, 프로젝트 세션에서 기준 프로젝트 PR/commit과 반영 범위를 먼저 정리한다.
- 사용자가 `지금 완료된 작업 wiki에 등록해줘.`처럼 짧게 요청해도, 현재 프로젝트 세션의 완료 작업 기준으로 wiki 반영 범위를 정리해 달라는 뜻으로 해석한다.
- 이때 사용자가 문서 경로, 반영 대상 문서, 세부 절차를 하나씩 지정하지 않아도 내부 규칙에 따라 후속 wiki 절차를 정리한다.
- wiki 반영 직전에는 wiki 로컬 `main`과 `origin/main`이 같은지 다시 확인한다.
- 프로젝트 세션에서 반영 범위를 정리하더라도, 실제 wiki 반영 브랜치 생성과 git 작업 대상 저장소는 wiki 저장소다.
- 상세한 브랜치 규칙과 반영 절차는 `wiki/AGENTS.md`를 따른다.

## AGENTS 작성 원칙
- `AGENTS.md` 계열 문서는 사람이 아니라 LLM이 먼저 읽는 실행 규칙 문서로 취급한다.
- 새 규칙을 추가할 때는 목적, 적용 범위, 판단 기준, 예외, 절차가 한눈에 구분되도록 짧은 섹션과 bullet 구조로 작성한다.
- 추상적인 표현보다 명령 순서, 기준 `branch + commit`, 허용/금지 조건처럼 기계적으로 해석 가능한 문장을 우선한다.
- 최신화 확인, 이슈 생성, 브랜치 생성처럼 서로 다른 흐름은 한 규칙에 섞지 않는다.
- `AGENTS.md` 계열과 사람용 사용자 문서가 충돌하면 `AGENTS.md` 계열을 기준 진실로 보고, 같은 브랜치와 같은 PR 범위에서 사용자 문서를 함께 정정한다.
- wiki 문서 정합성 검증이 필요한 변경은 작업 브랜치에서 실제 문서를 바로 수정하는 방식을 기본으로 한다.
- 단, 정합성 판단 기준은 수정 중인 워킹트리가 아니라 확인 가능한 `branch + commit`과 diff 단위로 설명한다.

## 줄바꿈 기준
- 저장소의 텍스트 파일 줄바꿈 기준은 `.gitattributes`를 따른다.
- 특별한 예외가 없으면 텍스트 파일은 `LF`로 작성한다.
- 줄바꿈 혼합(`mixed`) 상태가 보이면 같은 작업 범위에서 정규화한다.

## 규칙 변경 시 사용자 문서 동기화
- `AGENTS.md` 계열 또는 wiki 운영 규칙이 바뀌면 `wiki/Home/Wiki-Operating-Rules.md`와 `wiki/Home/Wiki-Usage-Guide.md`도 함께 검토한다.
- 변경된 규칙이 사람용 운영 설명, 요청 예시, 사용 절차에 영향을 주면 같은 작업 범위에서 함께 업데이트한다.
- 변경된 규칙이 사용자 요청 문장, 승인 흐름, 작업 순서 예시에 영향을 주면 `wiki/Home/Wiki-Usage-Guide.md`에 예시 요청을 최소 1개 함께 추가한다.
- 영향이 없어 사용자 문서를 수정하지 않으면 그 이유를 변경 요약이나 PR 본문에 짧게 남긴다.

## GitHub 작성 규칙
- PR이 같은 저장소의 이슈를 완전히 해결하면 PR 본문 `비고`에 `Closes #<번호>`를 적는다.
- 이슈를 완전히 닫지 않고 관련만 있거나 부분 반영이면 `Closes` 대신 `Refs #<번호>`를 적는다.
- 프로젝트 코드 관련 `issue`는 대상 코드 repo의 GitHub issue template을 따른다.
- wiki 저장소 자체 `issue`는 wiki 저장소 전용 변경 이슈 template을 따른다.
- wiki 규칙/가이드/운영 문서 수정 이슈 제목은 `docs: <주제>` 형식을 사용한다.
- 서로 다른 저장소의 issue template을 혼용하지 않는다.
- wiki 규칙/가이드/운영 문서 수정 PR의 `비고`에는 사용자 문서 동기화 여부, issue/template 변경 여부, 생략 사유를 함께 적는다.
- 새로 작성하는 GitHub `issue` 제목/본문, `PR` 제목/본문, 변경 요약은 기본적으로 한글로 작성한다.
- 다른 언어는 사용자가 명시적으로 요청한 경우에만 사용한다.
- wiki 규칙/가이드/운영 문서 수정 PR 제목은 `docs: <주제>` 형식을 사용한다.
- 프로젝트 PR 반영 wiki PR 제목은 `pr: <project-pr-number> <주제>` 형식을 사용한다.
- PR 본문 템플릿의 상세 규칙은 `wiki/AGENTS.md`를 따른다.

## 민감 정보 규칙
- 같이 쓰는 사람 전원이 봐도 되는 정보만 wiki에 올린다.
- 비밀번호, 토큰, API key, `.env` 값, 개인 연락처, 계정 식별자, 내부 URL/IP, 운영 DB 값은 올리지 않는다.
- 애매하면 민감 정보로 간주한다.
- 필요 시 `[REDACTED]`로 표시한다.
