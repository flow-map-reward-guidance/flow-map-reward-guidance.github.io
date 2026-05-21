# FMRG website — progress log

Working notes for the **project website** at
`flowmap-trajectory-guidance.github.io/index.html`. Read this + the file to
resume after context compaction.

---

## 1. What / where

- **Deliverable:** `index.html` (repo root) — single-page academic project
  site for the paper **"How to Guide Your Flow: Few-Step Alignment via Flow
  Map Reward Guidance" (FMRG)**. ~950 lines, self-contained.
- **Paper source (ground truth):** `/Users/jerryhuang/latex/flow_map_guidance (3)/arxiv/`
  (`abstract.tex`, `intro.tex`, `methods.tex`, `algorithmic.tex`,
  `experiments.tex`, `conclusion.tex`). `arxiv/figures` is a symlink →
  `../icml/figures`.
- **Curated paper figures:** `paper_assets/figures/` (named `figNN_*`) +
  `paper_assets/figures/appendix/`; manifest in `paper_assets/README.md`.
- **Blog:** `blog/index.html` exists (earlier full long-form build). The site
  links to it ("Blog →" / "Read the blog →"). NOTE: the blog predates the
  current design system and is **not yet restyled** to match — open item.
- **Backups:** `index.html.backup_YYYYMMDD_HHMMSS` in repo root.
- **Superseded drafts:** `index_styleA..G.html`, `index_v4.html`,
  `index_gallery.html`, etc. — ignore; `index.html` is the live one.
  (`index_v4.html` is still useful as the source of the curated carousel
  sample list — see §5.)

---

## 2. Design system (current)

Inspired by meta-flow-maps.github.io + proj-visual-thinking.jing.vision —
*principles, not copy*: figure-first, modular, restrained.

- **Type:** headings `Fraunces` (serif), body `Inter`, mono = SF Mono stack.
  - Section headers `<h2>`: serif ~1.78rem.
  - Subsection headers — `<h3>` **and** `.minihead` are unified into ONE
    style: serif **1.42rem** ("one modest step" below the section header).
  - **Body / reading text is uniform: 1rem (16px) Inter** — every paragraph,
    list item, card/problem/keypoint description, note, TL;DR. Driven by
    `body{font-size:1rem}`; use the single `1rem` token, never near-matching
    px values (a 17px-base vs 16px-`1rem` mismatch was a real bug). Body text
    is full `--text` colour, not muted.
  - Intentional size exceptions only: `.keyline` 1.2rem, `.qb-text` 1.16rem,
    and small captions/labels/tags (0.7–0.88rem). `.lede` is **body size
    (1rem)** — it is NOT larger; its only distinction is `font-weight:500`.
    The user repeatedly flagged a larger lede as inconsistent, so a lede now
    differs from body by weight alone, never size.
  - `.split.fig-cap` (the two Decision rows) is **1fr 1fr** — balanced, so the
    text column is not cramped. Was 1.25fr .75fr; the narrow text column made
    paragraphs run over awkwardly.
- **Color (`:root`):** `--text:#1c2030`; `--muted:#5a6076`; `--link:#5d52bd`;
  `--rule:#e6e5ee` (hairline); `--soft:#f5f5f8`; `--accent:#6e63cc`
  (lavender); `--tint:#f2f1fb`.
- **Box hierarchy — IMPORTANT, boxes must MEAN something (not all alike):**
  - **White + 4px accent left-bar** = top-tier "this matters" callout:
    `.tldrbox` (TL;DR), `.question-box` (central question), `.keypoint`
    (the optimal-control result box).
  - **Soft-grey (`--soft`) fill** = neutral equation/object panel: `.panel`.
  - **Lavender `--tint` fill** = the **"ours / FMRG"** identity — the
    `.eqpair` "ours" box, the FMRG row of the hierarchy box, `.stat` boxes.
    This is the sanctioned colored fill (earlier "never fill boxes" rule is
    superseded: fill now carries meaning).
  - **White + hairline card** (`.card`, radius 8px) = enumerated peer items
    (the 4 contributions).
  - **Top-rule + label, no box** (`.problem`) = supporting prose — the two
    Motivation "problems"; deliberately NOT a card.
  - `.keyline` = centered serif-italic pull-quote, not a box.
- **Hero wash:** `body` linear-gradient lavender wash behind the hero, fades
  to white by 640px. Hero widget itself all white.
- **Section header pattern:** `<span class="kicker">` = tiny uppercase
  tracked lavender label, format **"NN — Section name"** (e.g.
  "01 — Motivation") — orientation only. The `<h2>` under it is a
  **contentful headline** (a claim or question), never a synonym of the
  kicker. See §3.

---

## 3. Page structure (sections, in order)

Header pattern everywhere: kicker "NN — Name" (orientation) + `<h2>` = a
contentful headline (claim / question), so the two lines never echo.

1. **Sticky bar** `.bar` — brand + nav anchors: TL;DR · Motivation ·
   Contributions · **Key idea** · Method · Results · Blog → · BibTeX.
2. **Hero** `<header class="head">` — h1 "How to Guide Your *Flow*" (*Flow* in
   italic lavender), italic serif subtitle, authors (Jerry Y. Huang*, Justin
   Lin*, Sheel Shah, Kartik Nair, Nicholas M. Boffi — CMU), dark pill buttons.
   Buttons: **Paper** (arXiv link), **Code**, **BibTeX** — the separate
   "arXiv" button was dropped (it duplicated the Paper link).
3. **Hero widget** `#nfeWidget` — white card. FLUX.1-dev (left) vs +FMRG
   (right) before/after of the "abstract human form" aesthetic example.
   `Steps:` toggle 4/8/12 (default 8) + a t-scrubber + play. Closes with a
   `.wcap` italic caption (what the two panels are). See §4.
4. `#abstract` — **TL;DR** in a `.tldrbox` callout.
5. `#motivation` — kicker "01 — Motivation", h2 *"Samplers got fast. Guidance
   didn't."* (chosen for broad appeal — frames the gap any reader gets;
   "reward tilting" jargon is left to the panel/central-question below, where
   the section actually defines it). Opens with two **equal-size body paragraphs**
   (no lede — they sit adjacent, so a lede would clash; tailor samples to a
   reward $r$, then a sentence with **inline** reward examples — aesthetic
   quality / measurement / physical plausibility / human intent, emphasised
   inline, **no pills**);
   reward-tilt `.panel`; two `.problem` blocks in a `.problemgrid` (Hard to
   solve / A poor fit for modern samplers); `.question-box` central question.
6. `#contributions` — kicker "02 — Contributions", h2 *"From a new perspective
   to few-step alignment"*. 2×2 `.cards` grid: Guidance as optimal control /
   A unifying hierarchy / Theory that guides practice / Few-step alignment.
7. `#idea` — kicker "03 — Key idea", h2 *"So do we need the reward tilt?"*.
   Lede ("Not necessarily…"); `.eqpair` contrast (reward tilt → optimal
   control, "ours" box tinted); `.keypoint` callout "Exact optimal control"
   (shows the optimal control $u^*$, flow map highlighted); h3 subsection
   **"A hierarchy of approximations"** + intro; **hierarchy box**
   (Exact-optimal → FMRG → DPS; FMRG row tinted; arrows labelled); closing
   `.keyline` (DPS & its derivatives are coarse approximations of optimal
   control, not of the reward tilt).
8. `#method` — kicker "04 — Method", h2 *"Flow Map Reward Guidance"*. Lede on
   operator splitting; **method overview video** (the animated FMRG-vs-SMC
   schematic, in a figpanel); **operator-splitting
   panel** (flow-map step + guidance step); minihead "We arrive at two design
   decisions"; **Decision 1** (animated manifold SVG) + text; **Decision 2**
   (animated Gaussian canvas) + text. Both decision figures: the
   "Decision N — …" label sits **outside / above** the figure box. See §4.
   (The old centered "Read the blog →" line at the end of §04 was removed —
   the blog is reachable from the nav.)
9. `#results` — kicker "05 — Results", h2 *"Matches or surpasses baselines
   with as few as 3 NFEs"*. Lede; 4 result cards; **qualitative carousel**
   (`#qual`, reward-picker tabs); **quantitative carousel** (`#quant`,
   minihead "Quantitative results — tables & plots") — 4 slides: inverse-
   problems metrics (wide HTML table), LPIPS/FID-vs-NFE plot, GenEval HTML
   table, GenEval Pareto plot, each with a takeaway caption (`.qcapQ`, accent
   label + sentence). Caption labels carry **no "Table N / Figure N"
   numbering** (would go stale vs the paper). The inverse-problems table
   shows PSNR/SSIM/LPIPS/FID per task — **KID columns removed** for
   readability (12 data columns, not 15). The old
   `.qrow` (pareto img + simplified GenEval table) is gone — `.qrow` CSS is
   now unused, harmless.
10. `#bibtex` + footer.

---

## 4. Interactive / animated elements

All animations run only while on-screen (IntersectionObserver) and loop.

- **Method overview video** (`#methodVid`): `static/videos/fmrg_overview.mp4`
  (H.264, 1320×760, ~15.3 s, CRF 12, 25 fps) — the animated FMRG-vs-SMC schematic, replaces the
  old static `fig02_overview.png`. Muted, `playsinline`, no `loop`/`autoplay`;
  a small IIFE autoplays it once on the FIRST scroll into view; if scrolled
  away and back it resumes where it left off (never auto-restarts from 0), and
  a **Replay** button overlaid bottom-right (`#methodReplay`, `.vid-replay`)
  restarts it on demand — it does NOT loop (a build-up animation looping back
  to blank looks jarring), it rests on the finished diagram. `poster` =
  `fmrg_overview_poster.jpg` (final frame) — shown before play and for
  `prefers-reduced-motion` users (IIFE skips autoplay for them).
  NOTE: Playwright's headless Chromium can't decode H.264, so verify playback
  with a temporary VP9 webm; the shipped file stays mp4.
- **Hero step widget** (`#nfeWidget`, JS IIFE "Steps widget"): `trajImg` =
  current FMRG trajectory frame; frames preloaded from
  `static/images/abstract_human_form/traj/s{4,8,12}/NN.png` (5/9/12 frames).
  Scrubber `#trajRange` maps t∈[0,1] → frame. **Step toggle = cross-fade**
  (overlay `#trajFade` covers with old frame, fades out); **t-sweep & play =
  instant, no fade** (`clearFade()` on range input).
- **Decision 1 — manifold figure** (`#maniSvg`, JS IIFE "SVG draw-on"):
  the **exact paper figure**, inlined SVG. Built by instrumenting
  `flow_map_guidance (3)/icml/figures/manifold_anim.tex` (copy of
  `manifold_fig.tex` with `\special{dvisvgm:raw <g class="a-X">}` wrappers
  around each arrow group: `a-grad a-euc a-vpar a-dash a-jac`), compiled
  `latex` (DVI) → `dvisvgm`. Each group's shaft = the `path[fill='none']`;
  JS animates `stroke-dashoffset` (draw-on), fades in each arrowhead, then
  **pops in that arrow's text label (∇r, x₁ᴱ, v∥, x₁ᴶ) only after the arrow
  finishes drawing** (label = the group's `g[transform^="translate"]`);
  context labels (Tₓℳ, X_{t,1}, "reward increases") stay static.
  Sequence: ∇r → x₁ᴱ (off-manifold) → v∥ + dashed projection → x₁ᴶ
  (on-manifold). The `<image>` href is `static/images/manifold_blue.png`.
- **Decision 2 — Gaussian terminal distribution** (`#gwCanvas`, JS IIFE
  "Animated Gaussian"): `<canvas>` recreation (no source PDF/TikZ exists —
  only `gaussian_main_text.pdf`). λ FIXED; animates `t_stop` sweep 1.00→0.22
  loop. Curves: Reward r(x), Base ρ₁, Reward tilt, Greedy, Greedy + early
  stopping. Variances are the paper's closed forms; intermediate-t_stop
  variance uses the principled model σ(t_stop)=σ₁·exp(−πλσ₁·t_stop).
- **Qualitative carousel** (`#qual`, JS IIFE "Multi-reward"): 4 reward-family
  tabs; prev/next/dots/counter; touch-swipe.
- **Quantitative carousel** (`#quant`, JS IIFE "Quantitative results
  carousel"): static (no animation); 4 `.qslideQ` slides — 2 HTML tables
  (Table 9 / Table 13) + 2 paper plots (Fig 10 right / Fig 14); flex track +
  `translateX`; prev/next/dots/counter; touch-swipe. Each slide centers its
  artifact and a `.qcapQ` takeaway caption. Slide heights vary (table vs
  plot) but the flex track equalizes to the tallest, so no jump. Tables use
  the global `table` style; `tr.ours` = lavender `--tint`; `.best` bold
  accent, `.second` underline. Table 9 carries `.qtbl.wide` (smaller font,
  tight padding, `overflow-x:auto`); AFHQ/FFHQ row-group labels = `td.rgrp`
  (vertical text). Data + bold/underline transcribed exactly from the paper's
  `experiments.tex` (`tab:inverse_problems`, `tab:geneval`).

---

## 5. Assets

- `paper_assets/figures/` — `figNN_*` exact paper figures + `appendix/` +
  `manifold_anim.svg` (the instrumented Decision-1 figure).
- `static/images/`:
  - `carousel/` — 48 curated before/after PNGs (24 prompts ×
    `_unguided`/`_fmrg`). Human-preference carousel uses 18 of them (list
    taken from `index_v4.html`: abstracthuman, distantsilhouette, elderly,
    girlfloating, infinitelibrary, moonsiren, oceanbio, oceansky,
    snowsilence, ancienttemple, lonelyfog, diner, pastoral, redcar,
    forestwatercolor, jazz, lastnightsummer, celestial).
  - `vlm/` — 6 VLM panels; `style/` — style-hierarchy panels;
    `aesthetic/` — full 42-prompt set (not all used).
  - `inverse_main/` — the main-text inverse-problem grid, 9 cells (3 tasks ×
    Measurement/NFE 3/NFE 12). Source:
    `flow_map_guidance (3)/icml/figures/video_assets/inverse_problems_main_text/`
    (zoomed variants for SR + motion, plain for inpaint — matches the paper
    figure). The inverse-problems carousel tab is **3 `qslide trip` rows**,
    one per task (SR / motion deblur / inpaint), each = that column of the
    paper grid recast as a row.
  - `vlm/` VLM tab: **raccoon is the first slide**; 6 slides. Prompts are
    verbatim from the paper — raccoon/box/candles(`brass.png`)/clock-TV from
    `fig:vlm`, stop sign from the front-page figure `front_page_draft_v13.png`
    ("A stop sign that says FMRG!"). Tile-grid prompt is intentionally kept
    as-is (not in the paper). NOTE: `brass.png` actually depicts candles in
    brass holders — the filename is misleading, the prompt is the candles one.
  - `abstract_human_form/traj/s{4,8,12}/` — hero-widget trajectory frames.
  - `manifold_blue.png` — manifold background for the Decision-1 SVG.
- `static/videos/` — `fmrg_overview.mp4` (§04 method overview animation) +
  `fmrg_overview_poster.jpg` (its final frame). The mp4 is a recording of the
  HTML animation `animation/mid/FMRG_v6_asset/index.html`. Capture recipe
  (`/tmp/render_plain.py`): Playwright `record_video` at the **native
  1320×760 viewport** — do NOT enlarge the viewport (reflows the fixed-px
  panels) and do NOT use CSS `zoom` to fake 2×: the animation's final step
  `doFigure2()` draws the result-card "beams" from `getBoundingClientRect()`,
  and `zoom` skews those rects so the beams silently fail to draw.
  `device_scale_factor` is ignored by Playwright's video, so a true 2× capture
  isn't available — 1320×760 is the ceiling. Record long (~30 s) so the full
  timeline (build → SMC → `doFigure2` beams → ~4 s hold) is captured; the
  Playwright webm is 25 fps CFR, so encode `-r 25` (forcing 30 duplicates
  every 5th frame → judder). Trim load-in/tail, `ffmpeg -c:v libx264 -crf 12
  -pix_fmt yuv420p -r 25 -movflags +faststart`.

---

## 6. Rebuilding the manifold SVG (if it needs changes)

Edit `flow_map_guidance (3)/icml/figures/manifold_anim.tex`, then from the
`arxiv/` dir compile a wrapper:
`\documentclass[border=2pt,dvisvgm]{standalone}` +
`\usepackage[dvisvgm]{graphicx}` + tikz; run `latex` (NOT pdflatex →
DVI needed for `dvisvgm:raw` groups), then
`dvisvgm --no-fonts --exact --output=paper_assets/figures/manifold_anim.svg`.
After: re-point the `<image>` href to `static/images/manifold_blue.png`
(dvisvgm writes `figures/manifold_blue.png`). Re-inline into `index.html`.

Verify visually: `python3 -m http.server PORT` + Playwright screenshots.

---

## 7. Durable user preferences (design feedback)

- Minimal, clean, restrained; figures are the main character, text is
  bite-sized and packaged in compact forms (labels, ledes) — not prose walls.
- Don't blatantly copy reference sites — apply their *principles*.
- **Boxes must carry a visual hierarchy** — each box type means something
  (callout vs neutral panel vs "ours" vs card vs labelled prose); don't make
  them all look identical. See §2. Lavender tint fill = "ours".
- **Section headers:** kicker "NN — Name" (orientation) + a contentful h2
  headline (a claim or question); the two must never be synonyms.
- **Body text:** one uniform size (16px) and one family everywhere; only the
  lede / keyline / captions are intentionally different.
- Animations should be **drawn out**, not fade-revealed (except the hero
  step cross-fade). Arrow labels reveal *after* their arrow draws.
- Stay faithful to the paper; use only wording that appears in it (the user
  flags non-paper terms); capture FMRG-J vs FMRG-E and early stopping.

---

## 8. Open items / next steps

- **Blog** (`blog/index.html`) still uses the old design — restyle to the
  current system (Fraunces/Inter, lavender, white-hairline boxes) if desired.
- `fig01_front_page.png` (paper Fig 1 composite) is not shown on the site
  (the hero widget replaces it) — intentional, revisit only if asked.
- Real arXiv / GitHub URLs are placeholders (`https://arxiv.org/abs/`,
  `https://github.com/`).
- Mobile pass (done): no horizontal overflow at 390px. Fixes — hierarchy
  boxes stack to one column ≤560px; `.hl-eq` has `min-width:0;overflow-x:auto`
  so wide KaTeX equations scroll inside their box; the hero scrubber range
  input has `min-width:0` so the row no longer pushes `.tnow` off-screen.
  The `.split` two-column layouts still collapse at ≤680/760px.
