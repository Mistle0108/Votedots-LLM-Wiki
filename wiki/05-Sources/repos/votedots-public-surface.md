---
title: votedots-public-surface
type: source
status: active
updated: 2026-05-26
tags:
  - wiki
  - source
  - repo
  - public
  - landing
source_kind: repo-module
source_ref: votedots/main:public-surface
commit: ca5d4935b181dbd72e4895de5965b91ae7ae5d4a
---

# votedots-public-surface

## 목적
이 문서는 공개 landing, completed canvas, 정적 정보 페이지 관련 사실만 요약한다.

## 기준
| 항목 | 값 |
| --- | --- |
| Repo | `votedots` |
| Branch | `main` |
| Commit | `ca5d4935b181dbd72e4895de5965b91ae7ae5d4a` |
| Verified | `2026-05-26` |

## 확인 사실
- frontend router에는 `/`, `/ko`, `/en`과 locale별 `patches`, `roadmap`, `terms`, `privacy`, `community`, `contact` 공개 페이지가 있다.
- `/`는 locale redirect 페이지이고, `LandingPage`는 현재 광장 게임과 size/profile별 featured preview, completed canvas 미리보기를 함께 노출한다.
- 공개 완료 결과는 completed preview detail modal과 `public-canvas` final result 다운로드 엔드포인트로 이어진다.
- 공개 로그인 보드는 patch notes / roadmap 패널과 함께 login 화면에서 소비된다.
- 정적 공개 HTML과 `robots.txt`, `sitemap.xml`은 frontend build 전에 `sync:public-pages` 스크립트로 갱신된다.

## 주요 경로
| 계층 | 경로 | 사실 |
| --- | --- | --- |
| Frontend | `frontend/src/pages/landing/*` | locale landing, public updates, locale redirect 페이지를 제공한다. |
| Frontend | `frontend/src/pages/info/StaticInfoPage.tsx` | terms/privacy/community/contact 정적 정보를 렌더링한다. |
| Frontend | `frontend/src/features/landing/*` | landing API, featured preview, completed preview UI를 담당한다. |
| Frontend | `frontend/src/features/canvas-result/*` | 공개 결과 카드와 결과 modal UI를 담당한다. |
| Frontend | `frontend/src/features/login-board/*` | patch notes, roadmap, markdown 게시판 UI를 담당한다. |
| Frontend | `frontend/scripts/generate-public-pages.mjs` | locale별 정적 공개 페이지와 메타 출력을 생성한다. |
| Backend | `backend/src/modules/public-landing/*` | 공개 landing payload, completed preview, snapshot asset API를 담당한다. |
| Backend | `backend/src/modules/public-canvas/*` | final result 이미지와 고해상도 다운로드 API를 담당한다. |
| Backend | `backend/src/modules/login-board/*` | 공개 로그인 보드 데이터를 제공한다. |

## 주요 API 사실
| 엔드포인트 | 사실 |
| --- | --- |
| `GET /public/landing` | 현재 광장 게임과 featured game payload를 반환한다. |
| `GET /public/landing/previews` | landing preview 목록을 반환한다. |
| `GET /public/landing/completed` | 완료된 canvas 목록을 scope/date/page/sort 기준으로 반환한다. |
| `GET /public/landing/completed/:canvasId` | 완료된 canvas 상세 정보를 반환한다. |
| `GET /public/landing/previews/:previewId/asset` | preview asset을 제공한다. |
| `GET /public/landing/canvas/:canvasId/rounds/:roundId/snapshot` | 공개 round snapshot을 제공한다. |
| `GET /public/canvas/:canvasId/final-result` | 공개 final result 이미지를 제공한다. |
| `GET /public/canvas/:canvasId/final-result/download-hd` | 공개 final result 고해상도 다운로드 이미지를 제공한다. |
| `GET /public/login-board` | patch notes / roadmap 게시판 payload를 반환한다. |

## 연결 문서
- [[wiki/02-Architecture/System-Reference|System Reference]]
- [[wiki/02-Architecture/Data-Flow|Data Flow]]
- [[wiki/02-Architecture/Operations|Operations]]
- [[wiki/05-Sources/repos/votedots-lobby-room|votedots-lobby-room]]
- [[wiki/05-Sources/repos/votedots-history-summary|votedots-history-summary]]
