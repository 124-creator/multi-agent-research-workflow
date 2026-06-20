# ResearchLoop V4 · 双 Loop 多智能体协作工作流

ResearchLoop V4 把复杂科研、竞赛、论文和 AI 编程任务拆成两个闭环：

- **Loop 1 · 方案层**：先确认“做对的事”。通过问题冻结、风险地图、证据分级、候选路线、独立对抗评审、路线裁决和 Spike 验证，避免过早收敛到错误路线。
- **Loop 2 · 协同交付层**：再保证“把事做对”。通过同号调研台账、计划、复盘、核查、Test Oracle、Worktree Check 和三道人类门，把 Agent 交付变成可审计链路。

## 文件

| 文件 | 作用 |
|---|---|
| `000-dual-loop-controller-v4.md` | 全局总控：轨道选择、Loop 1、Loop 2、门禁、状态机与红线 |
| `010-claude-code-reviewer-v4.md` | Claude Code 审查官：仓库探索、计划级调研、plan、派工、终检 |
| `020-codex-executor-v4.md` | Codex 执行员：加载检查、执行前复核、隔离实现、测试、复盘与回传 |
| `../../apps/researchloop.html` | ResearchLoop HTML 原型：引导输入并生成 `010-问题定义.md` |
| `../../assets/researchloop-v4-flowchart.png` | V4 工作流总流程图 |

## 状态流

```text
draft -> approved -> implemented -> verified
```

- `draft`：计划草稿，不能执行。
- `approved`：通过 G2 执行门，可派发给执行员。
- `implemented`：执行员完成实现和测试，但尚未终验。
- `verified`：审查官终检 + 人类 G3 验收后成立。

## 三道人类门

- **G1 方向门**：确认问题定义和选定路线。
- **G2 执行门**：确认 plan、Test Oracle、隔离、回滚和外部写权限。
- **G3 验收门**：确认最终交付、终检证据和反证搜索。

