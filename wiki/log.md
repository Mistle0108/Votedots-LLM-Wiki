---
title: Wiki Log
type: log
status: active
updated: 2026-04-22
tags:
  - wiki
  - log
---

# log

## [2026-04-22] update | guard against PowerShell PR body mojibake
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/log.md`
- note: PowerShell 환경에서 한글 GitHub issue/PR 본문을 stdin이나 here-string 파이프로 직접 넘기지 않고, UTF-8 파일 기반으로 작성하도록 규칙을 추가했다. 이미 `??`처럼 깨진 본문은 같은 내용을 UTF-8 파일로 다시 업로드하는 방식으로 정정하도록 명시했다.

## [2026-04-22] update | formalize project-session wiki local-card setup
- updated: `AGENTS.md`
- updated: `README.md`
- updated: `raw/repos/AGENTS.md`
- updated: `raw/repos/_repo-local-card.template.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- added: `wiki/Home/Project-Session-Setup.md`
- updated: `wiki/index.md`
- updated: `wiki/log.md`
- note: 프로젝트 세션에서 local wiki 저장소를 기본 참조 환경으로 쓰는 규칙을 명시하고, `raw/repos/{repo}.local.md`의 `wiki_repo_path`를 1차 기준으로 고정했다. 경로가 없거나 접근이 안 되면 사용자에게 한 번만 확인한 뒤 local card에 저장하고 이후 기본값으로 재사용하도록 정리했으며, 이를 그대로 따라 할 수 있는 초기 세팅 문서를 추가했다.

## [2026-04-22] update | enforce UTF-8-safe wiki reading and docs issue title prefix
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `.github/ISSUE_TEMPLATE/wiki-change-template.md`
- updated: `wiki/log.md`
- note: 한글 문서는 처음부터 `git show` 또는 UTF-8 명시 읽기처럼 안 깨지는 경로로 확인하도록 규칙을 강화하고, 출력 인코딩을 바꿔가며 재시도하는 방식을 기본 경로에서 제외했다. wiki 규칙/가이드/운영 문서 변경 이슈 제목 prefix도 `[wiki]`가 아니라 `docs:`로 고정했다.

## [2026-04-22] update | front-load session usage prompts and simple wiki registration command
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `README.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/log.md`
- note: `wiki 어떻게 사용해?` 질문에는 문서 링크보다 세션에서 바로 쓸 수 있는 요청 예시를 먼저 안내하도록 정리하고, `지금 완료된 작업 wiki에 등록해줘.` 같은 짧은 명령을 현재 프로젝트 세션의 완료 작업 기준 wiki 등록 요청으로 해석하는 규칙과 사용자 안내를 추가함

## [2026-04-22] update | formalize wiki sync check and project-session workflow
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/log.md`
- note: wiki를 근거로 사용자 명령을 수행하기 전 로컬 wiki와 `origin/main` 일치 여부를 확인하는 규칙, 프로젝트 저장소 세션에서 wiki를 참조하는 운영 방식, 프로젝트 PR 완료 후 wiki 전용 브랜치와 PR로 반영하는 절차를 명문화

## [2026-04-22] update | prefer git object path reading for committed Korean markdown
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/log.md`
- note: PowerShell 인코딩 문제로 한글 문서가 깨질 수 있으므로, 커밋된 Markdown 원문은 기본적으로 `git show <ref>:<path>`로 읽고 미커밋 변경만 fallback으로 처리하는 규칙과 `AGENTS.md` / `wiki/AGENTS.md` 역할 분리를 명문화

## [2026-04-22] update | simplify wiki branch naming rules
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/log.md`
- note: wiki 반영 브랜치 규칙을 문서/운영 규칙 수정용 `docs/<topic-slug>`와 프로젝트 PR 반영용 `pr/<project-pr-number>-<topic-slug>` 두 가지로 단순화

## [2026-04-22] update | clarify wiki branch creation repo
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/log.md`
- note: 프로젝트 세션에서 반영 범위를 정리하더라도, wiki 반영 브랜치 생성과 wiki commit/PR/merge는 모두 wiki 저장소에서 진행한다는 규칙을 추가함

## [2026-04-22] update | formalize wiki sync commands and PR reflection checklist
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/log.md`
- note: wiki 동기화 확인 절차를 `git fetch origin main` -> `git rev-parse main` -> `git rev-parse origin/main` 기준으로 고정하고, 프로젝트 PR 반영 체크리스트와 `<topic-slug>` 규칙을 명문화함. 루트 `AGENTS.md`는 진입/요약 규칙 중심으로 더 얇게 정리함

## [2026-04-22] update | require Korean for newly written issue and PR content
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/log.md`
- note: 새로 작성하는 GitHub issue 제목/본문, PR 제목/본문, 변경 요약은 기본적으로 한글로 작성하고 다른 언어는 사용자가 별도 요청한 경우에만 사용하도록 규칙을 추가함

## [2026-04-22] update | clarify usage guide as human-facing document
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/log.md`
- note: `wiki/Home/Wiki-Usage-Guide.md`는 사람용 요청 예시 문서이고, LLM은 규칙 해석 시 `AGENTS.md` 계열 문서를 우선한다는 역할 분리를 명시함

## [2026-04-22] update | formalize wiki PR title and body templates
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/log.md`
- note: wiki PR 제목은 작업 성격에 따라 `docs: <주제>` 또는 `pr: <project-pr-number> <주제>` 형식을 사용하고, `docs`와 `pr`별 PR 본문 섹션 순서를 고정하는 규칙을 추가함

## [2026-04-22] update | strengthen git-object-first reading rule for committed Korean docs
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/log.md`
- note: 커밋된 한글 문서는 원칙적으로 처음부터 `git show <ref>:<path>`로 읽고, PowerShell 파일 읽기는 미커밋 변경·신규 파일·워킹트리 확인 같은 fallback 사유가 있을 때만 사용하도록 규칙을 강화함

## [2026-04-22] update | formalize sync mismatch handling with fast-forward main update
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/log.md`
- note: wiki 로컬 `main`과 `origin/main`이 다르면 먼저 불일치 사실을 알리고, 가능하면 로컬 `main`을 `origin/main`에 `fast-forward`로 맞춘 뒤 새 기준 commit으로 계속 진행하는 규칙과 예시 문구를 추가함. `main` 전환이나 `ff-only`가 실패하면 자동 merge/rebase는 하지 않도록 명시함

## [2026-04-22] update | add git show usage matrix
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/log.md`
- note: 커밋된 문서, 미커밋 변경, 신규 파일, 워킹트리 상태를 어떤 방식으로 읽어야 하는지 빠르게 판단할 수 있도록 `git show` / `git diff` / 파일 시스템 읽기 기준 표를 추가함

## [2026-04-22] update | wiki usage guide added
- added: `wiki/Home/Wiki-Usage-Guide.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/index.md`
- purpose: 팀원이 wiki를 언제 확인하고 언제 갱신해야 하는지, LLM에게 어떻게 요청해야 하는지 설명하는 사용 가이드 추가

## [2026-04-20] setup | raw/wiki/Output 구조와 index/log 초기화
- created: `raw/`, `wiki/`, `Output/`
- added: 루트 `AGENTS.md`, `wiki/index.md`, `wiki/log.md`, `wiki/07-Sources/README.md`
- moved: 기존 wiki 문서(`Home`, `01-Overview`~`06-Operations`)를 `wiki/` 아래로 재배치

## [2026-04-20] update | raw/repos source card 템플릿 추가
- updated: `raw/repos/AGENTS.md`
- added: `raw/repos/_repo-source-card.template.md`
- purpose: 실제 프로젝트 repo를 참조하는 기준 카드와 `repo ingest` 시작점 준비

## [2026-04-21] update | raw/repos 템플릿 placeholder 정리
- updated: `raw/repos/AGENTS.md`
- updated: `raw/repos/_repo-source-card.template.md`
- purpose: 경로/URL 같은 민감하거나 환경 의존 값이 `{PLACEHOLDER}`로만 남도록 템플릿 보완

## [2026-04-21] update | votedots repo source card 작성
- added: `raw/repos/votedots.md`
- fixed: 공용 설정값(`REPO_NAME`, `DEFAULT_BRANCH`, `PATH`, `MODULE`, `OPTIONAL_PATH`) 반영

## [2026-04-21] update | WSL repo path 기준 정리
- updated: `raw/repos/AGENTS.md`
- updated: `raw/repos/_repo-source-card.template.md`
- updated: `raw/repos/votedots.md`
- fixed: wiki는 Windows 경로, source repo는 WSL 경로를 함께 기록하도록 경로 기준 합의
- fixed: 실제 `repo ingest`는 `execution_path` 기준으로 수행하도록 정리

## [2026-04-21] ingest | votedots main repo bootstrap
- source: `votedots` `main@dfb53afe2dea21e75f74a33d9346d2ae60f7c890`
- policy: 미커밋 변경 제외, 사용자별 `execution_path` 기준 읽기
- updated: `raw/repos/votedots.md`
- added: `wiki/07-Sources/repos/votedots-overview.md`
- updated: `wiki/07-Sources/README.md`
- updated: `wiki/02-Current-State/README.md`
- updated: `wiki/03-System-Reference/README.md`
- updated: `wiki/04-Work-Tracking/README.md`
- updated: `wiki/index.md`

## [2026-04-21] update | development record 보강
- updated: `wiki/05-Development-Record/README.md`
- updated: `wiki/05-Development-Record/Worklog/README.md`
- updated: `wiki/05-Development-Record/Issues/README.md`
- updated: `wiki/05-Development-Record/Decisions/README.md`
- added: `wiki/05-Development-Record/Worklog/WK-2026-04-21-01-sparse-grid-chunk-rendering.md`
- added: `wiki/05-Development-Record/Worklog/WK-2026-04-14-01-summary-ready-flow.md`
- added: `wiki/05-Development-Record/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow.md`
- added: `wiki/05-Development-Record/Issues/ISS-001-large-canvas-full-grid-bottleneck.md`
- added: `wiki/05-Development-Record/Issues/ISS-002-automation-test-gap.md`
- added: `wiki/05-Development-Record/Decisions/DEC-001-sparse-grid-and-chunk-rendering.md`
- added: `wiki/05-Development-Record/Decisions/DEC-002-summary-ready-event-and-snapshot-flow.md`
- added: `wiki/07-Sources/prs/README.md`
- added: `wiki/07-Sources/prs/PR-233-sparse-grid-chunk-rendering.md`
- added: `wiki/07-Sources/issues/README.md`
- updated: `wiki/07-Sources/README.md`
- updated: `wiki/index.md`

## [2026-04-21] ingest | raw PR cards and PR source expansion
- added: `raw/prs/README.md`
- added: `raw/prs/_pr-source-card.template.md`
- added: `raw/prs/PR-233-sparse-grid-chunk-rendering.md`
- added: `raw/prs/PR-201-summary-ready-flow.md`
- added: `raw/prs/PR-182-game-entry-and-game-end-observe.md`
- added: `raw/issues/README.md`
- added: `raw/issues/_issue-source-card.template.md`
- added: `wiki/07-Sources/prs/PR-201-summary-ready-flow.md`
- added: `wiki/07-Sources/prs/PR-182-game-entry-and-game-end-observe.md`
- updated: `wiki/07-Sources/prs/README.md`
- updated: `wiki/07-Sources/README.md`
- updated: `wiki/index.md`
- note: issue 원문 링크/메타데이터는 아직 없어 `raw/issues`에는 template + ingest 준비 상태만 반영

## [2026-04-21] update | issue/pr 역할 규칙 명문화
- updated: `AGENTS.md`
- updated: `raw/issues/AGENTS.md`
- updated: `raw/prs/AGENTS.md`
- updated: `wiki/07-Sources/AGENTS.md`
- fixed: issue는 왜/무엇, PR은 어떻게/무엇이 바뀌었는지 기준으로 역할 분리
- fixed: issue/pr 중복 기록과 상호 링크 규칙을 운영 문서에 반영

## [2026-04-21] update | align ingest with GitHub templates (.github)
- source: `.github/ISSUE_TEMPLATE/*.md`, `.github/pull-request-template.md`
- updated: `AGENTS.md`
- updated: `raw/issues/README.md`
- updated: `raw/issues/AGENTS.md`
- updated: `raw/issues/_issue-source-card.template.md`
- updated: `raw/prs/README.md`
- updated: `raw/prs/AGENTS.md`
- updated: `raw/prs/_pr-source-card.template.md`
- updated: `wiki/07-Sources/issues/README.md`
- updated: `wiki/07-Sources/prs/README.md`
- purpose: issue/PR ingest 시 본문 구조 파싱 기준을 코드 repo `.github` 템플릿으로 고정

## [2026-04-21] ingest | GitHub open issues reflected into wiki
- source: `https://api.github.com/repos/Mistle0108/Votedots/issues?state=open&per_page=100`
- added: `raw/issues/ISSUE-234-history-panel-timeline.md`
- added: `raw/issues/ISSUE-212-outline-template-addition.md`
- added: `raw/issues/ISSUE-206-game-history-panel-snapshot-archive.md`
- added: `raw/issues/ISSUE-177-round-panel-intro-round-modal.md`
- added: `raw/issues/ISSUE-168-template-key-outline-canvas.md`
- added: `raw/issues/ISSUE-036-todo-backlog.md`
- added: `wiki/07-Sources/issues/ISSUE-234-history-panel-timeline.md`
- added: `wiki/07-Sources/issues/ISSUE-212-outline-template-addition.md`
- added: `wiki/07-Sources/issues/ISSUE-206-game-history-panel-snapshot-archive.md`
- added: `wiki/07-Sources/issues/ISSUE-177-round-panel-intro-round-modal.md`
- added: `wiki/07-Sources/issues/ISSUE-168-template-key-outline-canvas.md`
- added: `wiki/07-Sources/issues/ISSUE-036-todo-backlog.md`
- updated: `raw/issues/README.md`
- updated: `wiki/07-Sources/issues/README.md`
- updated: `wiki/07-Sources/README.md`
- updated: `wiki/05-Development-Record/Issues/README.md`
- updated: `wiki/02-Current-State/README.md`
- updated: `wiki/04-Work-Tracking/README.md`
- updated: `wiki/index.md`
- note: open issue는 source 문서에 사실만 정리하고, `code@commit` 해석은 current-state / work-tracking에 반영

## [2026-04-21] update | baseline commit moved to main@31d22b3
- source: `31d22b3535627b3a0a56ea1cf9e41411475f72fd`
- updated: `raw/repos/votedots.md`
- updated: `wiki/07-Sources/repos/votedots-overview.md`
- updated: `wiki/02-Current-State/README.md`
- updated: `wiki/03-System-Reference/README.md`
- updated: `wiki/04-Work-Tracking/README.md`
- updated: `wiki/07-Sources/README.md`
- updated: `wiki/index.md`
- note: `dfb53af..31d22b3` 범위에서 `.github/ISSUE_TEMPLATE/feature-template.md`, `.github/pull-request-template.md`만 변경됐고 애플리케이션 코드 변경은 확인되지 않음

## [2026-04-21] update | overview/home/operations baseline draft filled
- updated: `wiki/Home/README.md`
- updated: `wiki/01-Overview/README.md`
- updated: `wiki/02-Current-State/README.md`
- updated: `wiki/04-Work-Tracking/README.md`
- updated: `wiki/06-Operations/README.md`
- updated: `wiki/index.md`
- purpose: 팀이 wiki만 읽고 현재 상태, 다음 작업, 실행/운영 초안을 바로 파악할 수 있도록 빈 문서를 기준선 수준으로 보강

## [2026-04-21] update | repo ignore and auto-commit helper added
- added: `.gitignore`
- added: `scripts/auto-commit-wiki.ps1`
- purpose: `.obsidian` 로컬 파일을 제외하고, bootstrap 브랜치에서 wiki 변경을 한 번에 자동 커밋할 수 있는 기본 헬퍼 추가

## [2026-04-21] automation | wiki auto commit scheduled
- automation: `wiki-auto-commit`
- schedule: hourly
- policy: `main` 브랜치에서는 skip, 변경이 있을 때만 로컬 커밋, push는 하지 않음

## [2026-04-21] update | user-local repo path separated from shared docs
- updated: `AGENTS.md`
- updated: `raw/repos/AGENTS.md`
- updated: `raw/repos/_repo-source-card.template.md`
- added: `raw/repos/_repo-local-card.template.md`
- updated: `raw/repos/votedots.md`
- updated: `wiki/07-Sources/repos/votedots-overview.md`
- updated: `wiki/log.md`
- updated: `.gitignore`
- purpose: 사용자별 로컬 경로는 gitignored local card로 분리하고, shared wiki/raw 문서에는 고정 경로를 남기지 않도록 구조 보정

## [2026-04-21] update | local repo config simplified to execution_path only
- updated: `AGENTS.md`
- updated: `raw/repos/AGENTS.md`
- updated: `raw/repos/_repo-source-card.template.md`
- updated: `raw/repos/_repo-local-card.template.md`
- updated: `raw/repos/votedots.md`
- updated: `wiki/07-Sources/repos/votedots-overview.md`
- policy: LLM이 wiki를 읽고 ingest/update를 수행하는 운영 기준에 맞춰 개인 설정값은 `execution_path` 하나만 사용

## [2026-04-21] update | commit flow changed to user approval only
- updated: `AGENTS.md`
- removed: `wiki-auto-commit` automation
- policy: 기준 커밋으로 wiki 내용을 먼저 작성하고, 변경 요약 후 `커밋할까?` 동의를 받은 뒤에만 커밋

## [2026-04-21] verify | operations runbook checked against local environment
- checked: Windows Docker `28.3.2`, Docker Compose `v2.39.1-desktop.1`
- checked: `docker-compose.yml`, `docker-compose.prod.yml`, root/backend/frontend `.env.example`
- updated: `wiki/06-Operations/README.md`
- updated: `wiki/02-Current-State/README.md`
- updated: `wiki/04-Work-Tracking/README.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/index.md`
- result: Windows Docker는 설치돼 있지만 WSL integration 비활성 + `.env` 미준비로 실제 compose/health 검증은 완료하지 못함
## [2026-04-21] restructure | migrate wiki to document-first structure
- changed: top-level wiki structure from 1-Overview/02-Current-State/03-System-Reference/04-Work-Tracking/05-Development-Record/06-Operations/07-Sources
  to 1-Project/02-Architecture/03-Status/04-Records/05-Sources
- moved: existing status, architecture, records, and sources documents into the new folders
- updated: wiki/Home/README.md, wiki/index.md, wiki/AGENTS.md
- rewritten: section root docs for 1-Project, 2-Architecture, 3-Status, 4-Records, 5-Sources
- updated: wikilinks across wiki markdown files to match the new paths
- note: detailed record/source subdocuments were kept and linked into the new structure
## [2026-04-21] normalize | align records and source subdocs to new structure
- rewritten: wiki/04-Records/Worklog/README.md, wiki/04-Records/Issues/README.md, wiki/04-Records/Decisions/README.md
- rewritten: wiki/05-Sources/issues/README.md, wiki/05-Sources/prs/README.md
- updated: subfolder AGENTS.md files under 4-Records and 5-Sources
- normalized: lingering development-record tags and old link labels inside record detail documents
- note: detailed worklog / issue / decision / source pages were kept, with only naming and link cleanup applied
## [2026-04-21] add | architecture data-flow document
- added: wiki/02-Architecture/Data-Flow.md
- updated: wiki/02-Architecture/README.md
- updated: wiki/02-Architecture/System-Reference.md
- updated: wiki/Home/README.md
- updated: wiki/index.md
- note: documented auth/play, canvas/round/vote, summary/history flow as an architecture artifact
## [2026-04-21] expand | add repo module-level source documents
- added: wiki/05-Sources/repos/README.md
- added: wiki/05-Sources/repos/votedots-auth-play.md
- added: wiki/05-Sources/repos/votedots-canvas.md
- added: wiki/05-Sources/repos/votedots-round-vote.md
- added: wiki/05-Sources/repos/votedots-history-summary.md
- updated: wiki/05-Sources/repos/AGENTS.md
- updated: wiki/05-Sources/README.md
- updated: wiki/index.md
- updated: wiki/02-Architecture/System-Reference.md
- updated: wiki/02-Architecture/Data-Flow.md
- note: split repo source from one overview document into overview + module-level source documents for auth/play, canvas, round/vote, and history/summary
## [2026-04-21] update | formalize commit-based wiki baseline rule
- updated: AGENTS.md
- updated: wiki/AGENTS.md
- updated: wiki/Home/README.md
- note: fixed the rule that wiki must always be written against a specific ranch + commit, with code@commit as the primary truth and uncommitted changes excluded from the baseline

## [2026-04-21] update | formalize future issue/pr handling rule
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `raw/issues/AGENTS.md`
- updated: `raw/prs/AGENTS.md`
- note: 앞으로 생성되는 issue/pr은 모두 raw에 기록하고, status 문서는 영향이 있을 때 항상 갱신하며, detailed source/records는 재사용 가치가 있을 때만 선별 승격하도록 규칙을 고정했다.

## [2026-04-21] backfill | add historical PR context for history, intro, and outline/profile work
- added: `raw/prs/PR-210-separate-game-history-panel-from-canvas-page.md`
- added: `raw/prs/PR-202-intro-phase-guide-modal.md`
- added: `raw/prs/PR-173-canvas-config-profile-outline-template-log.md`
- added: `raw/prs/PR-172-outline-template-canvas-creation.md`
- added: `wiki/05-Sources/prs/PR-210-separate-game-history-panel-from-canvas-page.md`
- added: `wiki/05-Sources/prs/PR-202-intro-phase-guide-modal.md`
- added: `wiki/05-Sources/prs/PR-173-canvas-config-profile-outline-template-log.md`
- added: `wiki/05-Sources/prs/PR-172-outline-template-canvas-creation.md`
- added: `wiki/04-Records/Worklog/WK-2026-04-17-01-history-panel-separation.md`
- added: `wiki/04-Records/Worklog/WK-2026-04-14-02-intro-guide-modal.md`
- added: `wiki/04-Records/Worklog/WK-2026-04-10-01-outline-template-and-config-profile.md`
- added: `wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation.md`
- updated: `wiki/05-Sources/prs/README.md`
- updated: `wiki/04-Records/Worklog/README.md`
- updated: `wiki/04-Records/Decisions/README.md`
- updated: `wiki/03-Status/Current-State.md`
- updated: `wiki/03-Status/Next-Work.md`
- updated: `wiki/index.md`
- note: 현재 남아 있는 history / intro / templateKey-profileKey 과제의 배경이 되는 핵심 과거 PR과 기록을 backfill했다.

## [2026-04-21] backfill | add round snapshot storage and preview history
- added: `raw/prs/PR-211-round-snapshot-entity-and-storage-path.md`
- added: `raw/prs/PR-213-server-side-round-snapshot-preview-flow.md`
- added: `wiki/05-Sources/prs/PR-211-round-snapshot-entity-and-storage-path.md`
- added: `wiki/05-Sources/prs/PR-213-server-side-round-snapshot-preview-flow.md`
- added: `wiki/04-Records/Worklog/WK-2026-04-18-01-round-snapshot-storage-preview.md`
- updated: `wiki/05-Sources/prs/README.md`
- updated: `wiki/04-Records/Worklog/README.md`
- updated: `wiki/03-Status/Current-State.md`
- updated: `wiki/03-Status/Next-Work.md`
- updated: `wiki/index.md`
- note: history panel과 snapshot archive 과제의 기반이 되는 저장/preview 흐름 과거 이력을 backfill했다.
## [2026-04-21] expand | add data and infra repo source coverage
- added: wiki/05-Sources/repos/votedots-data-infra.md
- updated: wiki/05-Sources/repos/README.md
- updated: wiki/05-Sources/README.md
- updated: wiki/index.md
- updated: wiki/02-Architecture/Operations.md
- updated: wiki/03-Status/Current-State.md
- updated: wiki/03-Status/Next-Work.md
- note: moved migration/schema source coverage from planned to partial by adding a repo source for data source, session, storage, and prod dependencies

## [2026-04-21] expand | complete schema, persistence, and smoke-test documentation coverage
- added: `wiki/05-Sources/repos/votedots-schema-entities.md`
- added: `wiki/05-Sources/repos/votedots-summary-persistence.md`
- added: `wiki/02-Architecture/Smoke-Test-Scope.md`
- updated: `wiki/02-Architecture/README.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/index.md`
- updated: `wiki/03-Status/Current-State.md`
- updated: `wiki/03-Status/Next-Work.md`
- note: migration/entity 구조, summary/snapshot persistence, 핵심 smoke test 범위를 기준 커밋 문서로 고정했다.

## [2026-04-21] normalize | align operating rules and raw cards to the document-first structure
- updated: `AGENTS.md`
- updated: `raw/repos/AGENTS.md`
- updated: `raw/repos/_repo-source-card.template.md`
- updated: `raw/repos/votedots.md`
- updated: `raw/issues/README.md`
- updated: `raw/issues/AGENTS.md`
- updated: `raw/issues/_issue-source-card.template.md`
- updated: `raw/issues/ISSUE-036-todo-backlog.md`
- updated: `raw/issues/ISSUE-168-template-key-outline-canvas.md`
- updated: `raw/issues/ISSUE-177-round-panel-intro-round-modal.md`
- updated: `raw/issues/ISSUE-206-game-history-panel-snapshot-archive.md`
- updated: `raw/issues/ISSUE-212-outline-template-addition.md`
- updated: `raw/issues/ISSUE-234-history-panel-timeline.md`
- updated: `raw/prs/README.md`
- updated: `raw/prs/AGENTS.md`
- updated: `raw/prs/_pr-source-card.template.md`
- updated: `raw/prs/PR-182-game-entry-and-game-end-observe.md`
- updated: `raw/prs/PR-201-summary-ready-flow.md`
- updated: `raw/prs/PR-233-sparse-grid-chunk-rendering.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/03-Status/Current-State.md`
- note: raw 참조 카드와 운영 규칙에서 남아 있던 `07-Sources` / `05-Development-Record` / `02-Current-State` 경로를 새 구조(`05-Sources`, `04-Records`, `03-Status`)로 정규화했다.

## [2026-04-21] backfill | add play-entry and phase foundation history
- added: `raw/prs/PR-150-play-entry-route-and-auth-gate.md`
- added: `raw/prs/PR-151-game-phase-state-structure.md`
- added: `raw/prs/PR-153-phase-scheduler.md`
- added: `raw/prs/PR-156-gameplay-bootstrap-phase-alignment.md`
- added: `raw/prs/PR-157-phase-based-gameplay-ui-and-countdown.md`
- added: `raw/prs/PR-175-intro-phase.md`
- added: `wiki/05-Sources/prs/PR-150-play-entry-route-and-auth-gate.md`
- added: `wiki/05-Sources/prs/PR-151-game-phase-state-structure.md`
- added: `wiki/05-Sources/prs/PR-153-phase-scheduler.md`
- added: `wiki/05-Sources/prs/PR-156-gameplay-bootstrap-phase-alignment.md`
- added: `wiki/05-Sources/prs/PR-157-phase-based-gameplay-ui-and-countdown.md`
- added: `wiki/05-Sources/prs/PR-175-intro-phase.md`
- updated: `wiki/05-Sources/prs/README.md`
- updated: `wiki/04-Records/Worklog/WK-2026-04-11-01-play-entry-and-phase-flow.md`
- updated: `wiki/04-Records/Worklog/README.md`
- updated: `wiki/03-Status/Current-State.md`
- updated: `wiki/03-Status/Next-Work.md`
- updated: `wiki/index.md`
- note: `/play` 진입, game phase state, phase scheduler, gameplay bootstrap/ui, intro phase의 foundation 체인을 과거 PR 기준으로 backfill했다.

## [2026-04-21] backfill | add session-participant and realtime foundation history
- added: `raw/prs/PR-117-redis-active-session-management.md`
- added: `raw/prs/PR-118-session-based-participant-state.md`
- added: `raw/prs/PR-119-participant-count-and-list-api.md`
- added: `raw/prs/PR-120-round-participant-count.md`
- added: `raw/prs/PR-121-participant-panel-and-usertype-split.md`
- added: `raw/prs/PR-033-socket-handler.md`
- added: `raw/prs/PR-035-round-timer.md`
- added: `raw/prs/PR-041-live-vote-broadcast.md`
- added: `raw/prs/PR-057-vote-panel-foundation.md`
- added: `raw/prs/PR-058-frontend-socket-integration.md`
- added: `raw/prs/PR-059-round-ui-foundation.md`
- added: `wiki/05-Sources/prs/PR-117-redis-active-session-management.md`
- added: `wiki/05-Sources/prs/PR-118-session-based-participant-state.md`
- added: `wiki/05-Sources/prs/PR-119-participant-count-and-list-api.md`
- added: `wiki/05-Sources/prs/PR-120-round-participant-count.md`
- added: `wiki/05-Sources/prs/PR-121-participant-panel-and-usertype-split.md`
- added: `wiki/05-Sources/prs/PR-033-socket-handler.md`
- added: `wiki/05-Sources/prs/PR-035-round-timer.md`
- added: `wiki/05-Sources/prs/PR-041-live-vote-broadcast.md`
- added: `wiki/05-Sources/prs/PR-057-vote-panel-foundation.md`
- added: `wiki/05-Sources/prs/PR-058-frontend-socket-integration.md`
- added: `wiki/05-Sources/prs/PR-059-round-ui-foundation.md`
- added: `wiki/04-Records/Worklog/WK-2026-04-04-01-session-participant-foundation.md`
- added: `wiki/04-Records/Worklog/WK-2026-03-23-01-realtime-socket-round-vote-foundation.md`
- updated: `wiki/05-Sources/prs/README.md`
- updated: `wiki/04-Records/Worklog/README.md`
- updated: `wiki/03-Status/Current-State.md`
- updated: `wiki/03-Status/Next-Work.md`
- updated: `wiki/index.md`
- note: active session, participant state/count/panel, socket handler, round timer, vote broadcast, frontend socket UI foundation을 과거 PR 기준으로 backfill했다.

## [2026-04-21] update | clarify wiki operating rules and LLM read order
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/README.md`
- note: 저장소 구조 역할, 기준 진실 우선순위, 기존 페이지 우선 업데이트 이유, frontmatter 의미, `Current-State`와 `Next-Work` 차이, raw 갱신 시점, commit 이후 PR 요청 순서, `wiki 읽고 내용 확인해` 요청 시 LLM 기본 읽기 순서를 명시했다.

## [2026-04-21] add | team-shared wiki operating rules document
- added: `wiki/Home/Wiki-Operating-Rules.md`
- updated: `AGENTS.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/index.md`
- note: repo 3계층은 유지하고, 팀 공유 문서에서는 wiki 내부 구조와 문서 역할, LLM 읽기/쓰기 순서, ingest/update/publish 규칙을 카테고리별로 묶어 정리했다.

## [2026-04-21] fix | restore storage-structure wording and as-is block
- updated: `AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- note: `저장소 구조` 표현을 복원하고, 팀 공유 문서에 `raw / wiki / Output` 저장소 구조를 as-is 블록으로 명시했다.

## [2026-04-21] fix | simplify storage structure wording
- updated: `AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- note: 저장소 구조 설명을 `raw: 원본 또는 원본 참조 정보 / wiki: 공식 문서 / Output: 세션 결과, 임시 분석, 보고 초안`으로 단순화했다.

## [2026-04-21] update | refine log policy and remove as-is wording
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- note: `Wiki Operating Rules`의 `저장소 구조(as-is)` 표현을 `저장소 구조`로 정리했다. `log.md`는 사소한 문구 수정마다 기록하지 않고, ingest/backfill/구조 변경/상태 변경/규칙 변경처럼 의미 있는 업데이트 단위만 기록하도록 기준을 조정했다.

## [2026-04-21] update | clarify team-shared rules for log vs commit
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- note: 팀 공유 문서에서 `log.md`가 git commit 로그 대체물이 아니라 wiki 운영 로그임을 명시했다. `log.md` 기록과 git commit은 별개이며, 의미 있는 문서 변경은 커밋 전에도 기록 가능하다는 기준을 추가했다.

## [2026-04-21] update | allow AGENTS files as frontmatter exception
- updated: `AGENTS.md`
- updated: `wiki/AGENTS.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- note: 모든 공식 wiki 문서는 frontmatter를 유지하되, `AGENTS.md` 계열 운영 규칙 파일은 예외로 한다고 명시했다. 이유는 `AGENTS.md`가 catalog용 산출물 문서가 아니라 LLM 동작 규칙 파일이기 때문이다.

## [2026-04-21] restructure | split document roles and remove legacy guideline
- added: `README.md`
- updated: `AGENTS.md`
- updated: `wiki/Home/README.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- deleted: `WikiGuideLine.md`
- note: 문서 역할을 분리했다. 루트 `AGENTS.md`는 LLM 전역 규칙, `wiki/Home/README.md`는 wiki 진입점, `wiki/Home/Wiki-Operating-Rules.md`는 팀 공유용 운영 설명서, 루트 `README.md`는 저장소 첫 화면 안내로 정리했다. `WikiGuideLine.md`는 중복되는 구버전 가이드라 삭제했다.

## [2026-04-21] cleanup | remove unused auto-commit helper script
- deleted: `scripts/auto-commit-wiki.ps1`
- note: 현재 운영 기준은 자동 커밋이 아니라 사용자 승인 후 수동 커밋이므로, 더 이상 쓰지 않는 자동 커밋 헬퍼 스크립트를 삭제했다.

## [2026-04-22] update | add local path setup guidance to shared docs
- updated: `README.md`
- updated: `wiki/Home/Wiki-Operating-Rules.md`
- note: 팀원이 처음 저장소에 들어왔을 때도 개인 로컬 경로 설정 방법을 바로 찾을 수 있도록, 루트 `README.md`에는 짧은 안내를 추가하고 `Wiki Operating Rules`에는 `{repo}.local.md`와 `execution_path` 기준을 상세히 적었다.
