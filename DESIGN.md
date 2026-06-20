# Design

## Source of truth

- Status: Active
- Last refreshed: 2026-06-20
- Primary product surfaces: apps/researchloop.html, README.md, assets/researchloop-v4-flowchart.png, assets/researchloop-demo-preview.png.
- Protocol source of truth: docs/v4/000-dual-loop-controller-v4.md, docs/v4/010-claude-code-reviewer-v4.md, docs/v4/020-codex-executor-v4.md.
- Current design target: ResearchLoop V4.1 中文双循环动态控制台。
- Evidence reviewed:
  - The previous V4 page already had premium cards and basic interactions.
  - User clarified the core concept: Loop 1 is GPT-Pro producing/fixing plans while Claude independently reviews and gives modification advice; Loop 2 is Claude producing/reviewing plans while Codex executes, tests, and writes retrospectives.
  - The page must make these two loops visually and interactively obvious.

## Brand

- Personality: serious, frontier, audit-grade, calm under uncertainty, engineering-trustworthy.
- Trust signals: explicit role separation, independent review, feedback repair, execution isolation, retrospective report, evidence IDs, state machine.
- Avoid: generic process diagram, toy chatbot aesthetic, fake automation metrics, overclaiming real LLM execution in a static page, stale unrelated demo wording.

## Product goals

- Goals:
  - Within 10 seconds, show that ResearchLoop is a two-loop multi-agent governance system.
  - Make GPT-Pro, Claude, and Codex roles visually distinct.
  - Let visitors click nodes, step through the loop, and auto-play the cycle.
  - Make the workflow suitable for AI Agent internship portfolio review.
- Non-goals:
  - Do not call real LLM APIs.
  - Do not upload or collect user input.
  - Do not claim static simulation equals final human G3 acceptance.
- Success signals:
  - Clicking nodes changes active agent, action, artifact, evidence, and prompt.
  - Auto-play visibly moves through Loop 1, Loop 2, G3, and back to the next round.
  - The Chinese UI clearly explains both loops without reading the docs.

## Personas and jobs

- Primary personas: AI Agent / LLM engineering recruiter, technical interviewer, teammate who wants to reuse the workflow.
- User jobs: understand the two loops, inspect role responsibilities, see feedback repair, copy prompts, verify public safety.
- Key contexts of use: GitHub Pages, resume link click, interview screen share, mobile quick scan.

## Information architecture

- Primary navigation: 双循环、演示、证据链、提示词、完整图、GitHub.
- Core route: one-page static app at /ResearchLoop/ with source HTML at apps/researchloop.html.
- Content hierarchy:
  1. Hero: GPT-Pro × Claude × Codex two-loop value proposition.
  2. Dual-loop control room: clickable and auto-play core visualization.
  3. Detail cockpit: current agent, action, artifact, review signal, next step.
  4. Evidence and prompt linkage.
  5. Full V4 flowchart and repo call-to-action.

## Design principles

- Principle 1: The loop is the product. The central visualization must be a dynamic two-loop system, not a decorative image.
- Principle 2: Every click should change meaning. Node selection must update details, evidence, prompts, and status.
- Tradeoffs: Preserve static hosting and no-build simplicity over framework complexity.

## Visual language

- Color:
  - Deep ocean navy background: #07111f and #0f1d33.
  - Electric cyan for Loop 1 reasoning/plan repair: #2dd4ff.
  - Intelligent violet for Loop 2 execution/review: #8b5cf6.
  - Amber for review advice and risk: #f59e0b.
  - Emerald for pass/ready/G3 candidate: #10b981.
  - Red only for BLOCKER: #ef4444.
- Typography: system sans with Chinese-first readability; monospace for evidence IDs and prompt snippets.
- Spacing/layout rhythm: control-room density with large hero, 12-column responsive cards, 16/24/32px spacing.
- Shape/radius/elevation: rounded glass panels, orbital nodes, soft glow, high-contrast dark surfaces.
- Motion: flowing arrow accents, active node glow, auto-play pulse, reduced-motion respect.
- Imagery/iconography: CSS-native loop nodes plus existing flowchart image.

## Components

- Existing components to reuse: assets/researchloop-v4-flowchart.png.
- New/changed components:
  - Dual-loop orbital control room.
  - Auto-play and next-step controller.
  - Active step cockpit.
  - Review signal meter.
  - Evidence ledger linked to active node.
  - Prompt panel linked to active node.
  - Round state strip showing draft → reviewed → fixed → planned → implemented → reviewed → G3 → next round.
- Variants and states: active/inactive node, Loop 1/Loop 2, BLOCKER/RISK/PASS, idle/playing, copied prompt.
- Token/component ownership: inline CSS variables in apps/researchloop.html.

## Accessibility

- Target standard: practical WCAG 2.1 AA.
- Keyboard/focus behavior: all nodes are native buttons with focus-visible states.
- Contrast/readability: dark background with bright but controlled text contrast.
- Screen-reader semantics: headings, buttons, aria-live for active state.
- Reduced motion and sensory considerations: stop transitions under prefers-reduced-motion.

## Responsive behavior

- Desktop: central dual-loop visual with right cockpit and lower linked panels.
- Tablet: two-column cards collapse after cockpit.
- Mobile: single-column nodes grouped by loop; auto-play remains usable.
- Touch/hover differences: all hover-only affordances also appear as labels.

## Interaction states

- Loading: static page, no loading spinner needed.
- Empty: default active step is Loop 1 / GPT-Pro 方案草案.
- Error: clipboard copy failure falls back to visible button state.
- Success: copied prompt shows 已复制; pass states use emerald glow.
- Disabled: no disabled hidden controls; use explanatory text.
- Offline/slow network: static content remains useful after assets load.

## Content voice

- Tone: Chinese-first, precise, evidence-led, confident but not exaggerated.
- Terminology: ResearchLoop V4.1、方案校验循环、执行验证循环、独立检验、修改意见、执行计划、复盘报告、证据链、G3 验收.
- Microcopy rules: clearly state this is a static simulation; do not imply real execution without evidence.

## Implementation constraints

- Framework/styling system: single static HTML/CSS/JS file, no npm build required.
- Design-token constraints: CSS variables at top of HTML.
- Performance constraints: no external fonts/scripts; use existing flowchart and generated preview only.
- Compatibility constraints: modern Chrome/Edge/Safari/Firefox; GitHub Pages root deployment rewrites relative paths.
- Test/screenshot expectations: Playwright local and live checks, old-term scan, sensitive scan, screenshot preview.

## Open questions

- [ ] Future version may add a real backend executor; owner: Tian Zhongfei; impact: would need privacy policy and authentication.
