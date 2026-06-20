# 210 · ResearchLoop V4 top-tier demo upgrade plan

- Status: approved
- Plan ID: RL-V4-DEMO-210
- Revision: r2
- Date: 2026-06-20
- Basis: the user explicitly requested a top-tier, more beautiful GitHub demo page and asked to execute the plan to completion.

## Goal and scope

Upgrade ResearchLoop V4 from a static explainer into a GitHub portfolio-grade interactive product page, while fixing the README encoding/content issue. The page must accurately represent the V4 workflow and must not reuse stale unrelated demo wording.

## Work breakdown

1. T1 · Design contract and plan: refresh DESIGN.md and this approved plan.
2. T2 · Demo implementation: rewrite apps/researchloop.html with premium visual design, Task Lab, Flow Playback, Gate Simulator, Evidence Ledger, Case Study Replay, and Prompt Kit.
3. T3 · README landing page: rewrite README.md as a clean bilingual landing page with Live Demo, Preview, Quick Start, Privacy Boundary, protocol map, and repository map.
4. T4 · Preview image: generate assets/researchloop-demo-preview.png from the upgraded page.
5. T5 · Validation and deployment: run local browser checks, old-term scan, sensitive-info scan, push to GitHub, deploy GitHub Pages, and verify the live page.
6. T6 · Retrospective: write the execution retrospective using the V4 template style.

## Deliverable manifest

| # | Path | Action | Purpose |
|---|---|---|---|
| 1 | DESIGN.md | Modify | Design source of truth and visual system contract |
| 2 | docs/dev/plans/210-v4-demo-top-tier-upgrade-plan.md | Modify | Approved execution plan |
| 3 | apps/researchloop.html | Modify | Top-tier interactive V4 demo page |
| 4 | README.md | Modify | Clean repository landing page |
| 5 | assets/researchloop-demo-preview.png | Add | Demo preview for README and repository display |
| 6 | docs/retrospectives/2026-06-20-v4-demo-top-tier-upgrade.md | Add | Execution retrospective |

## Test Oracle

- apps/researchloop.html title includes ResearchLoop V4.
- Page contains and supports interaction for Task Lab, Flow Playback, Evidence Ledger, Gate Simulator, Case Study, and Prompt Kit.
- Browser load has no pageerror; key image loads successfully.
- Old-term scan returns zero hits for unrelated or stale wording.
- Sensitive scan does not find phone numbers, private email, tokens, local absolute paths, or private project-package wording in public files.
- README.md contains Live Demo, Preview, Quick Start, and Privacy Boundary without mojibake.
- GitHub Pages returns HTTP 200 and contains the new hero content.

## External writes

- Push main branch to GitHub.
- Force-push gh-pages branch with the static site build.
- Update repository homepage/topics if needed.

The user already authorized completing and syncing this GitHub demo work in the current thread.

## Isolation and rollback

- Modify only the deliverable manifest.
- Do not touch the user’s running project folders.
- Check git status before committing.
- Rollback with git revert for main and by redeploying the previous gh-pages commit if needed.
