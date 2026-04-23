# Votedots Wiki

이 저장소는 Votedots 프로젝트의 공식 wiki repo다.

시작 문서:
- [Home](wiki/Home/README.md)
- [Project Session Setup](wiki/Home/Project-Session-Setup.md)
- [Wiki Usage Guide](wiki/Home/Wiki-Usage-Guide.md)
- [Wiki Operating Rules](wiki/Home/Wiki-Operating-Rules.md)

세션에서 바로 쓰는 요청 예시:
- `wiki 읽고 현재 상태와 다음 작업 정리해줘.`
- `wiki에서 이 내용 확인해봐: <주제>`
- `wiki 기준으로 관련 문서 찾아줘: <주제>`
- `지금 완료된 작업 wiki에 등록해줘.`
- 마지막 요청은 현재 프로젝트 세션의 완료 작업 기준으로 wiki 반영 범위 정리 -> 대상 문서 확인 -> wiki 반영 절차 제안까지 이어지는 요청으로 본다.

LLM 운영 규칙:
- 프로젝트 세션에서 wiki 요청 해석과 경로 bootstrap 기준은 프로젝트 저장소의 `AGENTS.md`를 따른다.
- [AGENTS.md](AGENTS.md): wiki 저장소 루트 진입 규칙과 전역 기본값
- [wiki/AGENTS.md](wiki/AGENTS.md): wiki 내부 읽기/쓰기/publish 상세 규칙

개인 로컬 설정:
- 프로젝트 세션용 wiki 경로는 프로젝트 repo의 `./.local/wiki-repo.yml`에 저장한다.
- 현재 shell이 WSL이면 `wiki_repo_paths.wsl`, Windows shell이면 `wiki_repo_paths.windows`를 사용한다.
- wiki 경로를 한 번 확인하면 같은 파일의 현재 shell 슬롯에 저장하고 이후 기본값으로 사용한다.
- `raw/repos/{repo}.local.md`는 `execution_path` 같은 보조 로컬 메타데이터만 기록하며 git에 올라가지 않는다.
