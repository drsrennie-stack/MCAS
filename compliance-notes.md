# MCAS Compliance Notes

**Project:** MCAS (MedMasters Course Architecture System)
**Files covered:** `index.html`, `cvc-oei-rubric-audit.html` (v1.0 foundational framework)
**Date:** 2026-05-29
**Reviewer:** Dr. Sharilyn Rennie
**WCAG version / target:** 2.2, AA floor across the board, AAA on body text where achievable.

---

## 1. Scope

These files are the source of truth for branding and components in all MCAS-internal generators and the Architect app. They are not student-facing course deliverables. Faculty-facing course materials are out of scope and carry their own branding.

Both files inherit the BIO 004 course-home brand DNA: Plus Jakarta Sans only, no italics, no secondary fonts, alternating light/dark sections, MedMasters Collaborative logo lockup.

## 2. Color contrast audit

All ratios computed per WCAG 2.x relative luminance formula. Normal-text threshold: 4.5:1 (AA), 7:1 (AAA). Large-text (18pt+ or 14pt bold): 3:1 (AA), 4.5:1 (AAA).

| Pair | Use | Ratio | AA Normal | AAA Normal |
|---|---|---|---|---|
| Deep navy `#0B1530` on white `#FFFFFF` | Body on light section | 18.04:1 | PASS | PASS |
| Deep navy on cream `#F5F1E8` | (not used as bg; logo only) | 16.00:1 | PASS | PASS |
| Cream `#F5F1E8` on darker navy `#060A18` | Body on dark section | 17.50:1 | PASS | PASS |
| Oxblood `#8B3A2E` on white | Light-section accent text, eyebrows | 7.66:1 | PASS | PASS |
| White on oxblood | Rust primary CTA | 7.66:1 | PASS | PASS |
| White on rust-hover `#A0452F` | Rust CTA hover state | 6.20:1 | PASS | fail (passes AAA large) |
| Gold `#C9A14A` on darker navy | Dark-section accent, eyebrows | 8.16:1 | PASS | PASS |
| Deep navy on gold | Gold accent CTA | 7.46:1 | PASS | PASS |
| Terra `#C2734D` on darker navy | Headline accent on dark sections | 5.50:1 | PASS | fail (passes AA large) |
| Subtle border `#8C90A0` on white | Decorative card border | 3.18:1 | fail | fail |

### Notes on the audit

The new palette (BIO 004 reference) is substantially more accessible than the prior PRIMARY-spec palette. Every text/background pair passes WCAG AA at normal text size. Body pairs (navy on white, cream on darker navy) clear AAA by a wide margin.

The subtle border `#8C90A0` is purely decorative (1px card borders, dividers) and is not used for text. Decorative non-text contrast minimum is 3:1 per WCAG 1.4.11; this pair clears that bar.

## 3. Keyboard navigation flow

Verified in source for both files. Each interactive element is reachable in logical order via Tab:

1. Skip link (`-100px` until focused, then jumps to `#main`)
2. Site logo (links home)
3. Hero CTAs in order
4. Section content in document order (logo cards, swatches, comp cards, buttons, form fields with dropdowns first, table rows, list items, callouts, rules)
5. Footer links by column

Focus indicator is a 3px solid outline with 3px offset on every focusable element. On light sections the outline is oxblood `#8B3A2E`; on dark sections it switches to gold `#C9A14A`. No `outline: none` anywhere in the stylesheet.

## 4. Screen reader expectations

Verified at the markup level (live SR test recommended before any commercial release):

- Single `<h1>` per page (the hero headline), descending heading hierarchy throughout.
- Semantic landmarks: `<header>`, `<main id="main">`, `<section aria-labelledby>`, `<footer>`.
- Form inputs each have a real `<label for="…">` matched to `id`.
- Locked card carries `aria-disabled="true"`.
- Disabled button uses the native `disabled` attribute.
- Logo SVGs use `role="img"` with `aria-label`; decorative inline marks use `aria-hidden="true"`.
- Skip link is the first focusable element.
- Decorative `&middot;` separators are inline text and do not interfere with reading order.

## 5. Motion and sensory

- `@media (prefers-reduced-motion: reduce)` disables transitions and animations and resets `scroll-behavior` to auto.
- No autoplay, no parallax, no flashing or blinking content.
- Color is never the sole carrier of meaning. State variants (locked, unlocked, completed) combine border style (dashed vs. solid), border color, and fill weight so colorblind users can distinguish them by border treatment alone.

## 6. iframe-ready

Both files bake the height-sender script before `</body>`:
- `ResizeObserver` on `document.body`
- `load` and `resize` listeners
- Message id per-file (`mcas-component-index`, `mcas-cvc-oei-audit`)

All internal links use `target="_top"`. External links (when added) must use `target="_blank" rel="noopener"`.

## 7. Brand-rule compliance

- Plus Jakarta Sans Variable used exclusively. No Lora, no DM Sans, no JetBrains Mono in text. (Code blocks fall back to system monospace.)
- No italics anywhere. No `font-style: italic` in the stylesheet.
- No em dashes in any rendered text or source comment.
- Byline rule: `Dr. Sharilyn Rennie` with no credential suffix in every footer and signoff.
- Sage and cream are not in the page palette. Cream is reserved for text on dark sections only (and as a color inside the logo SVG).

## 8. Known limitations

- This is **v1, foundational framework**, not a polished commercial product. v2 will deliver: automated WCAG scoring, faculty-friendly form wrappers, MedMasters institutional branding layer, infographic flowchart, dashboard, RSI Engine, Accessibility Engine.
- Terra accent on dark passes AA normal at 5.50:1 but does not clear AAA. Accepted for accent-only use (headline-accent words, not body text).
- Rust-hover passes AA at 6.20:1 (vs. rust-rest at 7.66:1). Hover state is intentional UI feedback and is accepted at the lower ratio since both states pass AA.
- Live screen-reader testing should be repeated with NVDA + Firefox and VoiceOver + Safari before any external distribution.

## 9. Remediation plan

| Item | Action | Owner | Target |
|---|---|---|---|
| Live SR test | Run NVDA + Firefox, VoiceOver + Safari | Dr. Rennie | Before v2 |
| Print stylesheet | Print rules added to `cvc-oei-rubric-audit.html`; add equivalent to `index.html` | v2 build | v2 |
| Forced-colors mode | Audit against Windows High Contrast | v2 build | v2 |
| Automated scoring | Build WCAG scoring system per v2 spec | v2 build | v2 |

## 10. Sign-off

Both v1 files meet the global WCAG 2.2 AA floor. Body-text contrast clears AAA. Brand rules (Plus Jakarta only, no italics, no em dashes, byline rule, no student PII) are observed. Ready for use as the inheritance source for MCAS generators. Re-audit required before any v2 commercial release.

Reviewer: Dr. Sharilyn Rennie
