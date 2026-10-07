# HANDOFF - Arkana portfolio website (updated as work proceeds)

## Where everything is
- Working site (deploy-ready folder, NOT yet deployed): `C:\Documents\Arkana's Folder\Website\Template\vercel-deploy-patched\`
  - `index.html` (7 MB Claude Design "bundle": loader shell + base64 gzip asset manifest + one JSON-escaped page template), `vercel.json`, `favicon.svg`, `assets-web\` (78 images)
- Original exports (never modify): the `*.zip` files in `Template\`
- Live site (older design, deployed ~20 Sep): https://arkana-asido-portfolio-966bb5a8-385.vercel.app/
- Could NOT deploy from the session: no Node/Vercel CLI installed, MCP upload tool can't carry a 12 MB site. Options: install Node, run `npx vercel` in the folder (user does browser login), or re-publish from Claude Design.

## Already done in index.html (all tested)
- Head: title, lang=en, description, favicon, og/twitter tags, aria-label on logo link
- Missing assets fixed (assets-web folder added; 40 raw image paths)
- Mobile CSS (<=640px): nav CTA hidden, fixed-column grids collapse to 1 col; `html{overflow-x:hidden;overflow-x:clip}` safeguard
- Router: Back/Forward work (pushState + fromHistory flag); `window.__aaRoute` records current page
- Nav pill fix: bundled site-fx.js (manifest id ba33d1f6...) patched (single-run guard, route/hash-aware, adopts existing pill)

## Editing rules learned (IMPORTANT)
- Template is a JSON string inside `<script type="__bundler/template">`: quotes are `\"`, newlines `\n`, `</` is `<\u002F`. Edit with exact-once string replacement.
- In PowerShell, NEVER use Write-Output inside a function whose return value is assigned (it prefixed "ok:" log text to the file once). Verify file still starts with `<!DOCTYPE html>`.
- Assets in manifest are gzip+base64; to change a script: decode, edit, gzip, base64, swap into the `"data":"..."` of that id.
- Python from the session folder fails (Store python); serve from a TEMP copy: `python -m http.server <port>` and test in the browser pane. Browser pane hidden => animations freeze (measure target styles, not on-screen rects).
- Known pre-existing leftovers: none open for nav. Source `.dc.html` files in Portfolio-Site.zip are NOT patched; any copy change made only in index.html must be re-done in Claude Design or it will be lost on re-export.

## Current task (user request, 3 parts)
1. Full copywriting audit of the site; remove useless copy, rewrite weak copy. Style reference: https://www.dwihardiono.com/
2. Rebalance narrative: currently over-emphasizes short-form video / content creation. User wants ALL skills & experience emphasized evenly. Audit + fix immediately.
3. User attached a "20 things to do before launching your website" image. Decide which points apply, apply them, skip the rest.

### Status
- [~] reference site read - dwihardiono.com is blocked by the cloud proxy; style inferred (short, plain, concrete, no filler)
- [x] copy extracted + audited
- [x] copy edits applied (hero, tags, meta/title, about, card blurbs, CTA); narrative rebalanced to operations / events / communications / content / data
- [~] launch checklist - the "20 things" image is not in the repo; applied what is knowable (title, description, og/twitter, favicon, lang, robots.txt). Still open: custom domain + sitemap, analytics, 404 page, og:image size check, real Trakindo completion figures
- [ ] tested on mobile + copied to Template folder + deployed

## Progress log
- handoff created; no edits to copy yet.
- Edits applied via a script on the decoded template (json round-trip is byte-safe; keep `</` -> `<\u002F`). Deep copy on sub-pages (Visionaries / Ciputra / Bootcamp / Dempo) is still video-heavy and could be rebalanced next.
