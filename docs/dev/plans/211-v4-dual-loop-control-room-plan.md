# 211 · ResearchLoop V4.1 中文双循环动态控制台计划

- Status: approved
- Plan ID: RL-V4-DUAL-LOOP-211
- Revision: r2
- Date: 2026-06-20
- Basis: 用户明确要求优化页面，突出两个 Loop：Loop 1 为 GPT-Pro 方案生成/修复与 Claude 独立检验循环；Loop 2 为 Claude Plan/Review 与 Codex 执行/复盘循环，并要求页面更动态、更美观、以中文呈现。

## Goal and scope

将 ResearchLoop Demo 从高级说明页升级为中文双循环 Agent 工作流控制台。页面必须一眼看出两个循环的角色分工、反馈修复机制、执行复盘机制，并支持点击节点、下一步推进、自动播放、证据与提示词联动。

## Work breakdown

1. T1 · 计划与设计契约：新增本计划，刷新 DESIGN.md 中的 V4.1 视觉与交互约束。
2. T2 · 页面实现：重写 apps/researchloop.html，突出中文主界面、双 Loop 动态核心图、自动演示、节点联动、状态机、证据链、提示词联动。
3. T3 · README 更新：更新 README.md，说明 V4.1 双循环控制台和交互能力。
4. T4 · 预览图更新：重新生成 assets/researchloop-demo-preview.png。
5. T5 · 验证与部署：本地 Playwright、旧版无关词集合扫描、公开边界扫描、GitHub Pages 部署与远程浏览器核验。
6. T6 · 复盘：写入 docs/retrospectives/2026-06-20-v4-dual-loop-control-room.md。

## Deliverable manifest

| # | Path | Action | Purpose |
|---|---|---|---|
| 1 | DESIGN.md | Modify | 加入 V4.1 中文双循环控制台设计源事实 |
| 2 | docs/dev/plans/211-v4-dual-loop-control-room-plan.md | Add | 本 approved plan |
| 3 | apps/researchloop.html | Modify | 中文动态双 Loop 控制台页面 |
| 4 | README.md | Modify | 更新 V4.1 Live Demo、Preview、Quick Start 描述 |
| 5 | assets/researchloop-demo-preview.png | Modify | 新版页面预览图 |
| 6 | docs/retrospectives/2026-06-20-v4-dual-loop-control-room.md | Add | 本次执行复盘 |

## Test Oracle

- 页面 title 包含 ResearchLoop V4.1。
- 页面中文主界面包含：方案校验循环、执行验证循环、GPT-Pro、Claude、Codex、自动演示循环、下一步、证据链、提示词联动。
- 点击 Loop 1 节点后，详情面板、审查信号、证据链、提示词面板同步切换。
- 点击 Loop 2 节点后，详情面板、执行状态、证据链、提示词面板同步切换。
- 自动演示按钮能够推进至少 3 个不同节点；下一步按钮能够推进节点；到 G3 后能够回到下一轮 010。
- 本地浏览器无 pageerror / console error；关键图片加载成功。
- 旧版无关词集合扫描为 0。
- 公开边界扫描不命中凭据、私人联系方式、本地系统路径或非公开材料。
- README 包含 Live Demo、Preview、Quick Start、Privacy Boundary、双循环控制台。
- GitHub Pages 远程 HTTP 200，包含 V4.1 新内容，浏览器核验无错误。

## External writes

- Push main branch to GitHub.
- Force-push gh-pages branch to deploy the static site.
- Repository homepage remains https://124-creator.github.io/ResearchLoop/.

## Isolation and rollback

- 只修改 deliverable manifest 内文件。
- 不触碰用户正在运行的其他项目目录。
- Git 提交前执行状态检查与扫描。
- 回滚方式：git revert main commit；gh-pages 可重新部署上一版。
