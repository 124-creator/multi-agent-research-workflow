# 2026-06-20 · ResearchLoop V4 GitHub Sync Retrospective

## 1. What was done

- Synced the local ResearchLoop V4 workflow into the public repository.
- Added V4 protocol files under `docs/v4/`.
- Added the visual flowchart under `assets/`.
- Added the standalone ResearchLoop HTML prototype under `apps/`.
- Updated README, root contracts, architecture notes, templates, and examples.

## 2. Deliverables

| File / directory | Purpose |
|---|---|
| `docs/v4/` | V4 controller, reviewer, and executor instructions |
| `assets/researchloop-v4-flowchart.png` | Public workflow diagram |
| `apps/researchloop.html` | Spec generator prototype |
| `README.md` | GitHub landing page updated for ResearchLoop V4 |
| `AGENTS.md` / `CLAUDE.md` | Concise V4 executor/reviewer contracts |
| `templates/v4-*.md` | V4 plan and retrospective templates |
| `examples/010-problem-definition-example.md` | Frozen spec example |

## 3. Verification

- Repository status checked before sync: clean on `main`.
- Remote pulled with `git pull --ff-only origin main`: already up to date.
- Files copied from the local updated workflow folder.
- Final validation should include `git status`, `git diff --stat`, commit, push, and remote log verification.

## 4. Notes

This sync presents the repository directly as ResearchLoop V4: a dual-loop, evidence-graded, gated, and productized workflow for research and engineering delivery.
