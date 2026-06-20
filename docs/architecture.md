# ResearchLoop V4 Architecture Notes

ResearchLoop V4 separates complex Agent work into two loops:

- **Loop 1 · 方案层** answers whether the team is solving the right problem with the right route.
- **Loop 2 · 协同交付层** answers whether the approved route is implemented safely and verifiably.

## 1. Loop 1: do the right thing

Loop 1 produces a frozen, evidence-backed route before implementation starts.

| Step | Artifact | Purpose |
|---|---|---|
| 010 | 问题定义 | Freeze goal, success criteria, constraints, out-of-scope, knowns, unknowns |
| 012 | 难题风险地图 | Identify hard unknowns, risk types, escalation triggers |
| 015 | 调研基线与经验清单 | Gather official docs, upstream practices, GitHub/issue failures, skill candidates; grade evidence A/B/C/D |
| 020 | 候选路线 | Generate neutral candidate routes |
| 030 | 独立对抗评审 | Challenge candidates and calibrate BLOCKER vs RISK |
| 035 | 路线裁决 | Select route, dispose blockers, define module breakdown |
| 040 | 验证桩结论 | Run Spike A/B/C for feasibility, refutation, and integration |

## 2. Loop 2: do the thing right

Loop 2 makes execution auditable through same-numbered artifacts.

```text
research/NNN-模块中文名-调研台账.md
plans/NNN-模块中文名-计划.md
retrospectives/NNN-模块中文名-复盘.md
reviews/NNN-模块中文名-核查.md
```

The reviewer writes the plan and Test Oracle. The executor implements exactly what the approved plan permits. The reviewer then performs final review with fresh evidence and counter-evidence search.

## 3. Evidence IDs

ResearchLoop V4 uses explicit evidence IDs to avoid memory-based claims:

| Prefix | Source |
|---|---|
| `L1-E###` | Loop 1 evidence |
| `CC-R###` | Claude Code planning research |
| `CX-R###` | Codex execution research |
| `CC-V###` | Claude Code final verification evidence |

## 4. Human gates

- **G1**: approve the problem and route.
- **G2**: approve executable plan and external-write permissions.
- **G3**: accept final verified result.

## 5. State machine

```text
draft -> approved -> implemented -> verified
```

`implemented` is not `verified`. Verification requires final review and G3 acceptance.

## 6. Product prototype

[`apps/researchloop.html`](../apps/researchloop.html) is a standalone HTML prototype that turns project inputs into a structured `010-问题定义.md` document. It demonstrates how Spec Lock can be productized for students, research writers, modeling teams, and AI coding users.
