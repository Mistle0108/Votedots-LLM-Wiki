---
title: PR-172
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - outline
  - canvas
source_kind: pr
source_ref: PR-172
commit: 28ac004ca5f4e428eecd7bc4a3207cadcef8c6b3
---

# PR-172 outline template 정의와 canvas 생성 적용

## 문서 목적
이 문서는 merge commit `28ac004`에서 확인한 `#172` 관련 사실을 요약한다.

## 소스 기준
| 항목 | 값 |
| --- | --- |
| PR Reference | `#172` |
| Commit | `28ac004ca5f4e428eecd7bc4a3207cadcef8c6b3` |
| Date | `2026-04-10` |
| Basis | merge commit subject + changed files |

## 확인된 사실
- 커밋 제목은 `feat: 아웃라인 템플릿 정의 및 캔버스 생성 적용 로직 구현 (#172)`이다.
- 변경 파일은 `backend/src/modules/canvas/canvas.service.ts`, `backend/src/modules/canvas/template/outline-template.data.ts`, `outline-template.service.ts`, `outline-template.types.ts`다.
- outline template 데이터/서비스/타입 계층이 canvas 모듈 하위에 추가됐다.
- canvas 생성 서비스가 함께 수정돼 템플릿 선택 로직이 생성 흐름에 연결된 것으로 읽힌다.

## 관련 문서
- [[wiki/04-Records/Worklog/WK-2026-04-10-01-outline-template-and-config-profile|WK-2026-04-10-01]]
- [[wiki/04-Records/Decisions/DEC-003-outline-template-and-config-profile-separation|DEC-003]]
- [[wiki/05-Sources/issues/ISSUE-168-template-key-outline-canvas|ISSUE-168]]
