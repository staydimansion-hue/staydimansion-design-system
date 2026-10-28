# Staydimansion — Editorial Stay Design System

Source: `uploads/브랜드가이드.pdf` — a one-page brand guide (PDF, "Microsoft Print to PDF", single A4 page, text flattened to vector outlines — no copyable text or embedded fonts). Everything below was read visually off a high-resolution render of that page (colors were sampled pixel-for-pixel from the swatches; type sizes/line-heights in the scale table were too low-resolution to confirm exactly and are reconstructed to be internally consistent — flagged below).

Brand: **STAYDIMANSION**, tagline "머무는 시간을 편집하는 스테이" (a stay that edits the time you dwell in) — an "Editorial Stay" system built on quiet type, earth tones, and generous whitespace. No product screens were in the source; the guide's own "컴포넌트" (Components) section doubles as the closest thing to a UI kit, so the components and UI kit below rebuild that section faithfully.

**Logo (added 2026-09-19):** the source PDF had no mark, but the brand has a real logo: a circle divided by radial lines plus the wordmark DIMANSION, in `assets/logo/`. Use the supplied files, never redraw them. On Rust or Ink use `logo-horizontal-ivory.png`. Where a mark is not needed, the wordmark STAYDIMANSION set in Hahmlet caps with wide tracking is still fine.

**STAY DIMANSION logo (added 2026-10-21):** the lettering in the logo now reads **STAY DIMANSION** (two words). New files are `assets/logo/logo-stay-*.png`: `horizontal` (black on white), `horizontal-ink` and `horizontal-ivory` (tight-cropped, transparent), `stacked` (+ `-ink`, `-ivory`), and `overlay` (grey circle behind the word). `logo-symbol.jpg` has no lettering and is unchanged. Use these for new work; the old `logo-horizontal*.png` / `logo-stacked.png` say DIMANSION only. The new wordmark reuses the original D-I-M-A-N-S-I-O-N glyphs and the S and A of the original; the **T and Y were drawn to match** (same stem and hairline weights, same stroke contrast) because the original typeface is not known. If the original vector or font turns up, rebuild STAY from it.

**Decisions made after the source PDF (2026-09-19):**
- **No italic anywhere.** The PDF-derived scale listed Newsreader Italic for lead lines; the brand does not use italic. English lead lines and quotes use upright Hahmlet; Korean ones use Pretendard (see the no-Korean-serif decision below). Newsreader is no longer loaded.
- **English tagline:** "Stay with comfort, connect with ease." (used on the business card back). The Korean tagline "머무는 시간을 편집하는 스테이" stays.
- **Print exception to the 80/15/5 colour ratio:** the business card back is a full Rust field. Print pieces may use Rust as a background; screens still keep Rust for CTA and one emphasis.
- **No Korean serif (2026-10-28):** Korean text is always Pretendard (Noto Sans KR fallback), never Hahmlet or any serif. Serif is for English display text only. In CSS use `font-family: var(--font-display)` for English and `var(--font-body)` for Korean; the Latin-only Hahmlet subset in `fonts.css` means a Korean string wrongly set in the display stack still renders in Pretendard. Existing print files that set Korean in Hahmlet (business card name, rooftop notice title, kiosk POP lead, bread-bag sticker v1) predate this decision.
- **Korean line-breaking (2026-09-23):** always set `word-break: keep-all;` (plus `overflow-wrap: break-word;` as a fallback for one very long token) on Korean body copy. Default wrapping breaks a line between any two characters, which orphans a syllable — repeated user feedback calls this out. `tokens/base.css` sets it globally for production pages; a Design Component artboard is self-contained, so add the same rule to that artboard's own `<helmet><style> body{...}` block every time. **Exception (2026-10-14):** `keep-all` is for Korean only. On Japanese and Chinese blocks set `word-break: normal; line-break: strict;` (and `lang="ja"` / `lang="zh-Hans"`), otherwise they only break at punctuation. Wrap katakana words, key nouns and button labels in `white-space: nowrap` so they never split.

## Index
- `styles.css` — entry point, imports fonts + all tokens
- `fonts.css`, `tokens/colors.css`, `tokens/typography.css`, `tokens/spacing.css`, `tokens/print.css` (card size, bleed, CMYK builds, spot candidate), `tokens/base.css` (Korean keep-all line-breaking)
- `guidelines/` — foundation specimen cards (Colors, Type, Spacing, Brand, Logo, Print: CMYK builds and print spec)
- `components/` — Button, Input (text/date), SegmentedControl, Badge, RoomCard
- `ui_kits/booking-widget/` — the guide's booking widget + room card + quote + hours, recreated as a working screen
- `ui_kits/business-card/` — 90 x 50 mm business card, front and back (`index.html` preview, `print.html` print source)
- `assets/logo/` — logo files: `logo-stay-*` (STAY DIMANSION: horizontal, ink, ivory, stacked, overlay), the older DIMANSION-only horizontal / ivory / ink / stacked, and the symbol only
- `assets/print/` — the printed card PDF (CMYK, 96 x 56 mm, 3 mm bleed) and the CMYK / 별색 guide for Korean printers
- `tools/print-pdf/` — script and steps that turn `print.html` into the CMYK PDF
- `SKILL.md` — portable skill file for Claude Code

## Content fundamentals (말투 / Voice & Tone)
The guide gives an explicit do/don't list.

**이렇게 씁니다 (write this way):**
- Short sentences that end in plain periods
- No exclamation points or interjections — stay even-toned
- Be concrete about space and materials (e.g. oak, pine, weathered metal) instead of abstract adjectives
- Lead with the reason, not the pitch, and keep the register quiet/formal

**이렇게 쓰지 않습니다 (avoid):**
- Emoji, or inflated adjectives like "강력추천"/"완벽" (highly recommended / perfect)
- Excessive exclamation points or casual/spoken register
- Discount or deadline copy used as pressure tactics
- Unclear foreign loanwords used for flourish

**Worked example from the guide:** "오후 세 시에 문을 엽니다. 커피는 로비에 있고, 옥상은 밤 열한 시까지 열려 있습니다." (Opens at three in the afternoon. Coffee is in the lobby, and the rooftop stays open until eleven at night.) — plain declarative facts, no persuasion language, comma-joined clauses rather than short punchy fragments.

## Visual foundations
- **Color** — usage ratio is explicit in the guide: Page/Linen ~80%, Ink ~15%, Rust+Brass ~5% combined. Rust is reserved for CTAs and one emphasis element per screen; never body text. Brass fails contrast on Page (2.1:1) — decorative/icon use only, never text. Max ~2 accent uses per screen (one CTA + one highlight).
- **Type** — two families, each with one job: **Hahmlet (serif) for English display text only** — the wordmark, English titles, taglines, English lead lines and pull-quotes; **Pretendard for all Korean text** (headings at 600–700, lead lines at 500) and for UI and body copy. **No Korean serif, ever** (decided 2026-10-28; `fonts.css` loads a Latin-only Hahmlet subset so Hangul can never fall into it). No italic, no third family, no decorative display font. A bilingual layout sets the English line in Hahmlet and the Korean line in Pretendard. When Korean and Latin sit on one line, set the Latin about 10% larger (for example 9.5 px Korean, 10.5 px Latin) so they look the same size.
- **Backgrounds** — flat color fields only (Page / Page Deep / Linen / Ink). No photography treatment is defined in the source; no gradients, no patterns, no textures beyond a faint diagonal hairline texture used once as a placeholder fill in the applied-examples panel.
- **Borders & shadows** — no drop shadows anywhere in the source. Structure comes entirely from 1px hairlines (`--border-hairline`) and flat tone changes between adjacent fields. This is a stated principle: "각진 면, 얇은 선" (square faces, thin lines) — hierarchy via line + tone, not elevation.
- **Corner radii** — effectively square. Buttons and inputs show a very slight (2px) softening at most; cards and panels are sharp-cornered.
- **Spacing/grid** — 12-column grid, whitespace-first. Spacing scale is explicitly "multiples of 4."
- **Animation / hover / press** — not specified in the source (a static print guide). Components below use restrained, conventional treatments (opacity/tone shift on hover, no motion, no scale/bounce) to stay consistent with the brand's flat, quiet visual language — flagged as an intentional addition, not sourced.
- **Iconography** — none defined in the source. No icon font, no SVG set, no emoji. Treat the brand as icon-free until the user supplies one; don't introduce Lucide/Heroicons or hand-drawn glyphs without asking.

## Components (source-defined inventory)
The guide's "컴포넌트" panel shows: primary/secondary buttons, a date-range + guest-count search field, a 3-way segmented control, status badges/tags, a room card with price, a short pull-quote block, and an hours list inside a tab-style panel. Built as:
- `components/buttons/Button.jsx` — primary (solid ink) / secondary (outlined)
- `components/forms/Input.jsx` — text + date variants; `SegmentedControl.jsx`
- `components/feedback/Badge.jsx` — status tag (rust-filled "urgency" variant + outline variant)
- `components/cards/RoomCard.jsx` — image placeholder, name, copy, price, CTA

**Intentional additions:** none beyond the hover/press states noted above.

## Business card (added 2026-09-19)
Landscape 90 x 50 mm, two sides, built in `ui_kits/business-card/`.
- **Front:** Page background. Name in Pretendard 700 at 14 px (the version printed on 2026-09-19 used Hahmlet for the Korean name; reissue it this way if reprinted), then "총괄매니저 · General Manager". Phone and email at the lower left, aligned to the start of "General Manager"; the address at the lower right, right-aligned, ending with 스테이디멘션. No labels, no rules, no logo.
- **Back:** Rust background, ivory logo top centre, "STAY WITH COMFORT," bottom left, "CONNECT WITH EASE." bottom right (Hahmlet 500, 9 px, 0.12em tracking, caps).
- **Margins:** 13 px top/bottom and 15 px left/right from the trim line (3.4 to 4 mm). Do not go closer than 3 mm.
- **Contact standard for print:** phone 010-9730-4120, email staydimansion@gmail.com, address 인천광역시 미추홀구 인주대로131번길 6 스테이디멘션 (from the room rate sheet and house rules PDFs, 2026-09-19).

## POP / signage (added 2026-10-14)
Example: kiosk guide POP, an A5 piece printed on A4 paper.
- **Sheet:** A4 portrait, the A5 art (148 x 210 mm, 3 mm bleed) centred, crop marks outside the bleed (5 mm long, 3 mm from the trim), one line of cutting instruction below. Print at 100%, never "fit to page".
- **Layout:** logo top (ink, tight crop, 150 px wide), Korean lead sentence in Pretendard 600 28 px with one Rust rule above, Korean body 18 px, then one hairline-separated row per language (English, 日本語, 中文) with an 11 px label column. Korean is primary and largest; other languages 14.5 px.
- **Highlight:** the physical button label in Rust bold, one highlight per piece. Show the label as written on the device, in Korean, in parentheses after the translation, e.g. "CALL (호출)", so guests can match the button.
- **Source:** the print HTML is kept with the notices: `이성훈/클로드/공지/키오스크_호출_안내POP_A4_원본.html`.

## Print rules
- Work at 96 x 56 mm with 3 mm bleed; keep type and logo 3 mm inside the trim. Deliver CMYK PDF, text outlined.
- CMYK builds are in `tokens/print.css` and `guidelines/print-cmyk.html`. Type is single-plate K100. Page (C3 M4 Y10 K0) is a very light tint: on cream stock leave it unprinted.
- **Spot colour (별색):** Korean online printers mostly take CMYK only; spot needs offset and an extra plate. Rust candidates: PANTONE 7594 C (about #7C3A2D), alternative 7526 C (about #8A391B). Approximate matches, confirm on a swatch book and the real paper. Full notes in `assets/print/print-spec_CMYK_별색안내.pdf`.
- Known risk on the current card back: 6.8 pt reversed serif and 0.2 pt logo lines on 4-colour Rust can blur if plates shift. Use spot Rust, or enlarge.
- The PDF fonts are Hahmlet and Noto Sans KR because Pretendard could not be loaded in the export tooling. Rebuild with Pretendard if exact match matters (`tools/print-pdf/README.md`).

## Caveats — please help me get this right
- The PDF only yielded one flattened page at normal resolution; every color is pixel-sampled and exact, but the **type scale numbers (sizes/line-heights) are reconstructed**, not read with certainty — if you have the original file (Figma, InDesign, or a higher-res export), share it and I'll correct the scale.
- No icon set or photography is defined — flagged above rather than invented. (The logo was added later from `10_디자인/로고`.)
- The 12 px to 20 px body copy sizes and the print CMYK builds are conversions or estimates. The CMYK values use the Reference SWOP profile, not the printer's own.
- Animation/hover/press behavior isn't specified in a static print guide — what's built is a reasonable, conservative default. Tell me if the product should feel different (more editorial/slow, or snappier).
