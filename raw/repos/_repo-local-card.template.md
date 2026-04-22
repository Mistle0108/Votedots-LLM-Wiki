---
title: {REPO_NAME}-local
type: raw-repo-local-card
status: local
repo_name: {REPO_NAME}
execution_path: {EXECUTION_PATH}
wiki_repo_path: {WIKI_REPO_PATH}
---

# {REPO_NAME}-local

## 목적
- 이 문서는 개인 로컬 환경에서만 쓰는 실행 경로 카드다.
- git에 올리지 않고, 실제 `repo ingest` 전에만 참조한다.

## 규칙
- `execution_path`: 실제 명령 실행 기준 경로
- `wiki_repo_path`: 프로젝트 세션에서 참조할 local wiki 저장소 경로
- 사용자 계정명이나 WSL 경로처럼 개인 환경에 종속된 값만 넣는다.
- 프로젝트 세션이 WSL 경로를 쓰면 `wiki_repo_path`도 WSL에서 보이는 경로로 적는다.
- wiki 경로를 한 번 확인했다면 그 값을 `wiki_repo_path`에 저장하고 이후 기본값으로 재사용한다.
- 공용 wiki / raw 카드에는 이 값을 다시 복사하지 않는다.
