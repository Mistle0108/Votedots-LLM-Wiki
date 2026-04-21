---
title: PR-233
type: source
status: active
updated: 2026-04-21
tags:
  - wiki
  - source
  - pr
  - canvas
source_kind: pr
source_ref: PR-233
commit: dfb53afe2dea21e75f74a33d9346d2ae60f7c890
---

# PR-233 sparse grid + chunk ?뚮뜑留?援ъ“ ?꾪솚

## 臾몄꽌 紐⑹쟻
??臾몄꽌??merge commit `dfb53af` 硫붿떆吏? 蹂寃?踰붿쐞?먯꽌 ?뺤씤??`#233` 愿???ъ떎???붿빟?쒕떎.

## ?뚯뒪 湲곗?
| ??ぉ | 媛?|
| --- | --- |
| PR Reference | `#233` |
| Commit | `dfb53afe2dea21e75f74a33d9346d2ae60f7c890` |
| Date | `2026-04-21` |
| Basis | merge commit subject + changed files |

## ?뺤씤???ъ떎
- 而ㅻ컠 ?쒕ぉ? `???罹붾쾭????묒쓣 ?꾪븳 sparse grid + chunk 湲곕컲 ?뚮뜑留?援ъ“ ?꾪솚 (#233)`?대떎.
- 蹂寃?踰붿쐞?먮뒗 `frontend/src/features/gameplay/canvas/*`, `frontend/src/pages/canvas/model/*`, `backend/src/modules/canvas/*`, `backend/src/modules/history/*`媛 ?ы븿?쒕떎.
- ???뚯씪濡?`frontend/src/features/gameplay/canvas/hooks/useChunkLoader.ts`媛 異붽??섏뿀??
- ?뺤쟻 諛곌꼍 asset ?뚯씪??異붽??섏뿀??
- commit 硫붿떆吏?먮뒗 `viewport 湲곕컲 chunk ?붿껌 ?쒖뼱`, `chunk-based canvas cell query api`, `sparse persistence`, `snapshot 湲곕컲 ?쒖떆` ?먮쫫???곗냽 ?묒뾽?쇰줈 ?멸툒?쒕떎.

## 愿??臾몄꽌
- [[wiki/05-Sources/repos/votedots-overview|votedots-overview]]
- [[wiki/04-Records/Issues/ISS-001-large-canvas-full-grid-bottleneck|ISS-001]]
- [[wiki/04-Records/Decisions/DEC-001-sparse-grid-and-chunk-rendering|DEC-001]]

