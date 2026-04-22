---
title: PR-173
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - canvas
  - profile
  - outline
source_kind: pr
source_ref: PR-173
commit: be07d4ff43c98c0acc8986b82839bbb8ab0e4347
---

# PR-173 config profile + outline template 로그

## 문서 목적
이 문서는 merge commit `be07d4f`에서 확인한 `#173` 관련 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#173` |
| Commit | `be07d4ff43c98c0acc8986b82839bbb8ab0e4347` |
| Date | `2026-04-10` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: 캔버스 프로파일 기반 설정과 outline 템플릿 로그 추가 (#173)`다.
- 변경 파일에 `backend/src/config/game-config-profiles/*`, `backend/src/config/game.config.ts`, `backend/src/database/migrations/1778000000000-AddCanvasConfigFields.ts`, `backend/src/entities/canvas.entity.ts`, `backend/src/modules/canvas/*`, `frontend/src/features/gameplay/session/*`, `frontend/src/shared/config/game-config.ts`가 포함된다.
- 백엔드에는 game config profile 파일 분리, canvas config field 추가 migration, canvas entity/controller/service 수정이 들어갔다.
- 프론트엔드에는 gameplay session/bootstrap, canvas model, shared config 계층 수정이 함께 들어갔다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-10-01-outline-template-and-config-profile|WK-2026-04-10-01]]
- [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]]
- [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]]
- [[wiki/05-Sources/issues/ISSUE-212-outline-template-addition|ISSUE-212]]
