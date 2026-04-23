---
title: Project Session Setup
type: project-session-setup
status: active
updated: 2026-04-23
tags:
  - wiki
  - home
  - setup
---

# Project Session Setup

## 목적
- 이 문서는 프로젝트 세션에서 local wiki 저장소를 기본 참조 대상으로 쓰기 위한 초기 세팅 방법을 설명한다.
- 목표는 사용자가 프로젝트 세션에서 `wiki 최신 상태 확인해줘`, `지금 완료된 작업 wiki에 등록해줘.`처럼 짧게 요청해도 local wiki 저장소가 안정적으로 매핑되게 만드는 것이다.

## 언제 필요한가
- 처음 local wiki 저장소를 연결할 때
- wiki 저장소 경로가 바뀌었을 때
- 프로젝트 세션 shell이 Windows에서 WSL로, 또는 WSL에서 Windows로 바뀌었을 때

## 핵심 원칙
- 프로젝트 세션에서 local wiki 저장소 경로의 1차 기준은 프로젝트 저장소의 `./.local/wiki-repo.yml`이다.
- 현재 shell이 WSL이면 `wiki_repo_paths.wsl`, Windows shell이면 `wiki_repo_paths.windows`를 확인한다.
- 현재 shell 슬롯에 값이 있고 현재 세션에서 접근 가능하면 그 값을 기본 wiki 경로로 사용한다.
- 현재 shell 슬롯 값이 없거나 접근할 수 없으면 사용자에게 경로를 한 번만 확인하고, 같은 파일의 현재 shell 슬롯에 저장한 뒤 이후 기본값으로 재사용한다.
- `raw/repos/{repo}.local.md`는 `execution_path` 같은 보조 로컬 메타데이터용이며, wiki 경로 bootstrap 1차 기준으로 쓰지 않는다.
- 환경 변수나 shell 초기화 파일 설정은 필수로 두지 않는다.
- 프로젝트 `execution_path`가 WSL이면 wiki 경로도 WSL에서 보이는 경로를 쓴다.

## 준비할 값
- 프로젝트 repo 루트 경로
- 프로젝트 repo 실행 경로
- 현재 shell 종류(WSL / Windows)
- 현재 프로젝트 세션 shell에서 보이는 wiki 경로

## 세팅 순서
1. local wiki 저장소 경로를 현재 프로젝트 세션 shell 기준으로 확정한다.
2. 프로젝트 저장소에 `./.local/wiki-repo.yml`을 만들고, `.local/` 또는 최소 해당 파일이 gitignored 상태인지 확인한다.
3. 현재 shell 슬롯(`wiki_repo_paths.wsl` 또는 `wiki_repo_paths.windows`)에 wiki 경로를 기록한다.
4. 이후 프로젝트 세션에서는 먼저 같은 슬롯 값을 읽고, 접근 가능한지 확인한다.
5. 슬롯 값이 없거나 접근이 안 될 때만 사용자에게 한 번만 다시 확인하고, 같은 슬롯 값을 갱신한다.
6. 프로젝트 세션에서 wiki 경로와 sync 확인이 바로 되는지 검증한다.

## 경로 작성 기준
- WSL shell이면 `wiki_repo_paths.wsl`에 `/mnt/...` 형태 경로를 적는다.
- Windows shell이면 `wiki_repo_paths.windows`에 `P:\...` 형태처럼 Windows에서 바로 여는 경로를 적는다.
- 같은 사용자라도 shell이 바뀌면 다른 슬롯 값을 따로 저장해야 할 수 있다.

## 프로젝트 로컬 설정 예시
- 예시:

```yaml
version: 1
repo_name: votedots
wiki_repo_paths:
  wsl: /mnt/p/03_Project/VotedotsWiki
  windows: P:\03_Project\VotedotsWiki
```

- 이 파일은 프로젝트 저장소의 `./.local/wiki-repo.yml`에 두고 git에 올리지 않는다.
- 한 번 확인한 wiki 경로는 같은 파일의 현재 shell 슬롯에 저장해 이후 기본값으로 재사용한다.

## wiki repo 보조 로컬 카드
- `raw/repos/{repo}.local.md`는 여전히 개인 로컬 카드로 유지하되, `execution_path` 같은 실행 경로 메타데이터만 관리한다.
- 템플릿 파일은 `raw/repos/_repo-local-card.template.md`다.
- 프로젝트 세션의 wiki 경로 1차 기준으로는 이 파일을 쓰지 않는다.

## 추천 검증 요청문
```text
프로젝트 세션에서 `./.local/wiki-repo.yml`의 현재 shell 슬롯 기준으로 local wiki repo 경로를 먼저 확인하고,
git fetch origin main 기준으로 wiki 최신 상태와 기준 commit 확인해줘.
```

```text
프로젝트 세션에서 project-local wiki 설정 기준 local wiki repo 경로 resolve 순서와 현재 기준 경로를 먼저 말해줘.
그다음 wiki 최신 상태를 확인해줘.
```

## 문제 해결
- `./.local/wiki-repo.yml`이 없으면:
  - 프로젝트 저장소에 파일을 만든다.
  - 현재 shell 기준 경로를 한 번 확인해 해당 슬롯에 저장한다.
- 현재 shell 슬롯 값은 있는데 경로 접근이 안 되면:
  - 현재 프로젝트 세션 shell에서 보이는 경로인지 다시 확인한다.
  - Windows 경로와 WSL 경로를 섞어 적지 않았는지 확인한다.
  - 확인한 새 값을 같은 파일의 현재 shell 슬롯에 다시 저장한다.
- `raw/repos/{repo}.local.md`만 있고 project-local 설정 파일이 없으면:
  - local card를 wiki 경로 1차 기준으로 쓰지 않는다.
  - 프로젝트 저장소의 `./.local/wiki-repo.yml`을 새로 만든다.

## 한 줄 요약
- 프로젝트 세션에서 wiki 저장소 경로의 핵심 기준은 프로젝트 저장소의 `./.local/wiki-repo.yml`이다.
- 경로를 한 번 확인하면 같은 파일의 현재 shell 슬롯에 저장하고 이후 기본값으로 재사용한다.
