# MCAS Compliance Notes

**Project:** MCAS (MedMasters Course Architecture System)
**Files covered:** `index.html` (v1.0 foundational framework, component index)
**Date:** 2026-05-29
**Reviewer:** Dr. Sharilyn Rennie
**WCAG version / target:** 2.2, AA floor across the board, AAA on body text where achievable.

---

## 1. Scope

This index is the source of truth for branding and components in all MCAS-internal generators and the Architect app. It is not a student-facing deliverable. Faculty-facing course materials are out of scope and carry their own branding.

## 2. Color contrast audit

All ratios computed per WCAG 2.x relative luminance formula. Normal-text threshold: 4.5:1 (AA), 7:1 (AAA). Large-text (18pt+ or 14pt bold): 3:1 (AA), 4.5:1 (AAA).

| Pair | Use | Ratio | AA Normal | AAA Normal |
|---|---|---|---|---|
| Navy `#1E3D4C` on white `#FFFFFF` | Body text on cards | 11.49:1 | PASS | PASS |
| Navy on off-white `#FAFAF9` | Body on page bg | 11.01:1 | PASS | PASS |
| Navy on navy-tint `#EDF1F3` | Completed-state card text | 10.11:1 | PASS | PASS |
| Terra-dark `#A0522D` on white | Eyebrow, H2/H3 | 5.62:1 | PASS | fail (passes AAA large) |
| Terra-dark on off-white | Eyebrow on page bg | 5.38:1 | PASS | fail (passes AAA large) |
| Gray-700 `#374151` on white | Body card text, hints | 10.31:1 | PASS | PASS |
| Gray-500 `#6B7280` on white | Captions, small meta | 4.83:1 | PASS | fail |
| White on navy | Primary button | 11.49:1 | PASS | PASS |
| White on navy-deep `#142A36` | Primary button hover | 14.85:1 | PASS | PASS |
| Navy-deep on gold `#B8924A` | Accent CTA (fixed) | 5.13:1 | PASS | fail |
| Code text `#E8EEF1` on navy | Code blocks | 9.81:1 | PASS | PASS |

### Fix applied during audit

White on gold (`#FFFFFF` on `#B8924A`) measured at **2.90:1**, which fails AA at every text size. The `.btn--accent` rule was updated to use **navy-deep text on gold** (5.13:1, passes AA). Hover state preserves the same text/background combination and signals interactivity through border color and elevation rather than color change.

### Known constraint

Terra-dark for eyebrow text (12px, 600 weight) passes AA normal at 5.62:1. AAA normal would require deepening terra-dark further, which would drift from the brand. Eyebrow text remains AA-compliant; this is documented and accepted.

## 3. Keyboard navigation flow

Verified in source. Each interactive element is reachable in logical order via Tab:

1. Skip link (visible on focus, jumps to `#main-content`)
2. TOC links in document order
3. Card CTAs in grid order
4. Button row, left to right
5. Form fields in form order: Course dropdown, Module dropdown, Tool type dropdown, Title input, Notes textarea, three checkboxes, three radios, Generate, Reset

Focus indicator is a 3px brushed-gold outline with 2px offset on every focusable element (`:focus-visible`). No `outline: none` anywhere in the stylesheet.

## 4. Screen reader expectations

Verified at the markup level (live SR test recommended before any commercial release):

- Single `<h1>` per page, descending heading hierarchy.
- Semantic landmarks: `<header role="banner">`, `<nav aria-label="Section navigation">`, `<main id="main-content">`, `<footer role="contentinfo">`.
- All form inputs have a real `<label for="...">` matched to `id`.
- Locked card carries `aria-disabled="true"`.
- Disabled button uses the native `disabled` attribute.
- Decorative `&middot;` separators are inline text and do not interfere with reading order.

## 5. Motion and sensory

- `@media (prefers-reduced-motion: reduce)` collapses animation and transition durations to 0.01ms.
- No autoplay, no parallax, no flashing content.
- Color is never the sole carrier of meaning. State variants (locked, unlocked, completed) combine border style, border color, and fill so that a colorblind user can distinguish them by border treatment alone.

## 6. iframe-ready

Height-sender script is baked in before `</body>`:
- `ResizeObserver` on `document.body`
- `load` and `resize` listeners
- One-shot post on script load
- Message id: `mcas-component-index` (downstream generators must use their own id)

All internal links use `target="_top"`. There are no external links in this file; when added, they must use `target="_blank" rel="noopener"`.

## 7. Known limitations

- This is **v1, foundational framework**, not a polished commercial product. Limitations carried forward into v2 planning: no automated WCAG scoring, no faculty-friendly form wrappers, no MedMasters institutional branding layer, no infographic flowchart, no dashboard.
- AAA on terra-dark eyebrows not pursued (brand constraint).
- Screen reader testing should be repeated with NVDA + Firefox and VoiceOver + Safari before any external distribution.

## 8. Remediation plan

| Item | Action | Owner | Target |
|---|---|---|---|
| Live SR test | Run NVDA + Firefox, VoiceOver + Safari | Dr. Rennie | Before v2 |
| Print stylesheet | Add `@media print` rules | v2 build | v2 |
| Forced-colors mode | Audit against Windows High Contrast | v2 build | v2 |
| Automated scoring | Build WCAG scoring system per v2 spec | v2 build | v2 |

## 9. Sign-off

Foundational framework meets the global WCAG 2.2 AA floor with one documented AA-only (non-AAA) exception on eyebrow text. Ready for use as the inheritance source for MCAS generators in v1. Re-audit required before any v2 commercial release.

Reviewer: Dr. Sharilyn Rennie
