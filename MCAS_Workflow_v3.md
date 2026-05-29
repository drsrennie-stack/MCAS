# MCAS Workflow v3 — Locked Spec

Date: 2026-05-29
Author: Dr. Sharilyn Rennie

This document locks the streamlined faculty workflow for the MedMasters Course Architecture System. Builds on the project update PDF dated 2026-05-29.

## The system in one line

Great courses aren't generated. They're architected.

## Three inputs, one engine, one course package

```
Faculty Brand Sheet  (HTML app, 1 per faculty)   → how the course should feel
+ Master Course Workbook (xlsx,   1 per course)  → what should be built
+ Prototype Selection    (1 per course)          → how the course should be organized
────────────────────────────────────────────────
                   MCAS Engine
────────────────────────────────────────────────
                  Course Package
```

## Faculty workflow

1. **Build your Brand Sheet once.** Open `faculty-branding-app.html`. Fill the 10 sections. Export `.brand.json`. Reuse across every course you teach. Update only when your teaching identity actually changes.

2. **Open a new Master Course Workbook per course.** Duplicate `MCAS_Master_Course_Workbook_v3.xlsx`. Rename with the course code, e.g. `MCAS_BIO-431_Fall-2026.xlsx`. Save to your project folder.

3. **Fill tab 01 Course Setup.** Course code, title, term, modality, faculty name, byline, start/end dates, weeks, **Prototype Selection** (dropdown), Brand Sheet filename. This is the only place course-level metadata lives.

4. **Fill tab 02 Faculty Brand Summary.** Point to the `.brand.json` filename. Drop in 10 summary fields (palette name, fonts, AI rules, WCAG target). The full interview stays in the HTML brand sheet; no duplication.

5. **Architect the course on tabs 03–09.** Learning Outcomes, Asset Library (with per-deliverable Format + Convert-to-HTML flag), Schedule & Pacing, Module Builder, Assessments, Engagement, Lab Components.

6. **Run the Compliance Phase on tabs 10–12.** Accessibility (WCAG 2.2 AA floor), RSI evidence, Quality Assurance. The pre-seeded QA and Launch tasks give you the standard checklist.

7. **Close out on tab 13 Launch Checklist.** Sign-offs, dry-run, embed test.

8. **Upload to the MCAS Engine.** Workbook + Brand Sheet JSON. Pick prototype. Engine produces the course package.

9. **Adjust through the semester.** The workbook is the operating document. Edits propagate to the dashboard live.

## Per-deliverable format choice

Asset Library and Assessments tabs both have a **Format** column (HTML / DOCX / PDF / PPTX / Slide deck / Video / Audio / Image / External link / Other) and a **Convert to HTML?** flag (Yes / No / N/A).

Faculty pick per item. If they flag **Yes**, the MCAS Engine generates the asset as accessible HTML and accessibility is handled by the platform (iframe-ready, WCAG 2.2 AA baked in). If **No**, they keep the original format and the Accessibility tab tracks their manual audit.

## Prototypes (locked architecture)

Each prototype is a fixed structural template. Accessibility, RSI scaffolding, navigation, and component patterns are baked in. Faculty pick one per course; they don't redesign these.

1. Traditional Online
2. Hybrid
3. Team-Based Learning (TBL)
4. Case-Based
5. Accelerated
6. Competency-Based
7. Course Redesign / Program Review

Detailed Prototype Specifications are the next development priority (per the Project Update PDF).

## What changed from v2

- **One workbook per course** (was a multi-course tracker).
- Tab names match the Project Update PDF: `01 Course Setup`, `02 Faculty Brand Summary`, `04 Asset Library`.
- **Prototype Selection** added to tab 01 with dropdown.
- **Format** + **Convert to HTML?** columns added to Asset Library and Assessments.
- **Lab Components** tab added (was missing).
- Tab 02 collapsed from the full 10-section interview to a 12-field pointer that references the HTML Brand Sheet by filename.
- Dashboard simplified to a single-course readiness scorecard (counts + WCAG/RSI/QA/Launch %).
- Pre-seeded standard QA checks and Launch tasks.

## File inventory

| File | Role | Faculty action |
|---|---|---|
| `faculty-branding-app.html` | Input 1: Brand Sheet builder | Fill once, export `.brand.json`, reuse |
| `MCAS_Master_Course_Workbook_v3.xlsx` | Input 2: Course architecture | Duplicate per course, fill, save, adjust through term |
| (Prototype Selection) | Input 3: Structural template | Pick on tab 01 dropdown |
| `master-course-builder.html` | MCAS Engine UI (in progress) | Upload Workbook + Brand JSON; engine produces course |
| `accessibility-engine.html` | Compliance Phase tool | Run against the generated course package |

## Open work

1. Detailed Prototype Specifications for each of the 7 prototypes. **Next priority per Project Update PDF.**
2. Wire `master-course-builder.html` to actually ingest a Workbook + Brand JSON and emit a Course Package.
3. Future workbook dashboard features: faculty workload analysis, student workload analysis, readiness score formulas (current dashboard has WCAG % and Launch %; RSI score and QA score still to add).

## Notes on branding

Per the Project Update PDF dated 2026-05-29: MCAS branding uses Plus Jakarta Sans, Navy #0B1530, Rust #8B3A2E, Gold #C9A14A, Cream #F5F1E8, Dark #060A18. The Workbook v3 uses these. The Brand Sheet HTML currently uses the PRIMARY teaching palette (#1E3D4C navy, #B8924A gold, #C2734D terra); a palette repaint to align with the new MCAS spec is queued but out of scope for this streamlining pass.
