---
title: Project Session Setup
type: project-session-setup
status: active
updated: 2026-04-22
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
- 프로젝트 세션에서 local wiki 저장소 경로의 1차 기준은 `raw/repos/{repo}.local.md`의 `wiki_repo_path`다.
- `wiki_repo_path`가 있고 현재 세션에서 접근 가능하면 그 값을 기본 wiki 경로로 사용한다.
- `wiki_repo_path`가 없거나 접근할 수 없으면 사용자에게 경로를 한 번만 확인하고, 같은 파일에 저장한 뒤 이후 기본값으로 재사용한다.
- 환경 변수나 shell 초기화 파일 설정은 필수로 두지 않는다.
- 프로젝트 `execution_path`가 WSL이면 wiki 경로도 WSL에서 보이는 경로를 쓴다.

## 준비할 값
- 프로젝트 repo 실행 경로
- local wiki 저장소 경로
- 현재 프로젝트 세션 shell에서 보이는 wiki 경로

## 세팅 순서
1. local wiki 저장소 경로를 현재 프로젝트 세션 shell 기준으로 확정한다.
2. wiki 저장소의 `raw/repos/{repo}.local.md`를 만들어 `execution_path`와 `wiki_repo_path`를 함께 기록한다.
3. 이후 프로젝트 세션에서는 먼저 `wiki_repo_path`를 읽고, 접근 가능한지 확인한다.
4. 경로가 없거나 접근이 안 될 때만 사용자에게 한 번만 다시 확인하고, 같은 파일 값을 갱신한다.
5. 프로젝트 세션에서 wiki 경로와 sync 확인이 바로 되는지 검증한다.

## 경로 작성 기준
- 프로젝트 `execution_path`가 WSL 경로면 wiki 경로도 `/mnt/...` 형태로 적는다.
- 프로젝트 세션이 Windows shell이면 wiki 경로도 `P:\...` 형태처럼 Windows에서 바로 여는 경로를 적는다.
- 같은 사용자라도 shell이 바뀌면 `wiki_repo_path`를 현재 shell 기준 경로로 다시 맞춰야 할 수 있다.

## local card 설정 예시
- 템플릿 파일: `raw/repos/_repo-local-card.template.md`
- 예시:

```yaml
---
title: votedots-local
type: raw-repo-local-card
status: local
repo_name: votedots
execution_path: /home/<user>/Votedots
wiki_repo_path: /mnt/p/03_Project/VotedotsWiki
---
```

- `execution_path`와 `wiki_repo_path`는 둘 다 개인 환경값이므로 git에 올리지 않는다.
- 한 번 확인한 wiki 경로는 이 파일의 `wiki_repo_path`에 저장해 이후 기본값으로 재사용한다.

## 추천 검증 요청문
```text
프로젝트 세션에서 local card의 `wiki_repo_path`와 local wiki repo 경로를 먼저 확인하고,
wiki 로컬 main과 origin/main 동기화 여부 확인해줘.
```

```text
프로젝트 세션에서 local card 기준 local wiki repo 경로 resolve 순서와 현재 기준 경로를 먼저 말해줘.
그다음 wiki 최신 상태를 확인해줘.
```

## 문제 해결
- `wiki_repo_path`가 없으면:
  - 프로젝트 세션에서 경로를 한 번 알려준다.
  - 확인한 값을 같은 파일에 저장한다.
- `wiki_repo_path`는 있는데 경로 접근이 안 되면:
  - 현재 프로젝트 세션 shell에서 보이는 경로인지 다시 확인한다.
  - Windows 경로와 WSL 경로를 섞어 적지 않았는지 확인한다.
  - 확인한 새 값을 `wiki_repo_path`에 다시 저장한다.

## 한 줄 요약
- 프로젝트 세션에서 wiki 저장소 경로의 핵심 기준은 `raw/repos/{repo}.local.md`의 `wiki_repo_path`다.
- 경로를 한 번 확인하면 같은 파일에 저장하고 이후 기본값으로 재사용한다.
