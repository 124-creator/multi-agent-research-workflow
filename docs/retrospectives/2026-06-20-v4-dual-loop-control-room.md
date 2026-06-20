# ResearchLoop V4.1 中文双循环动态控制台复盘

### 复盘块 · 任务 T1-T6 · V4.1 中文双循环控制台 · 2026-06-20

- 对应 plan 任务 / 路线部分：RL-V4-DUAL-LOOP-211 · T1 计划与设计契约、T2 页面实现、T3 README、T4 预览图、T5 验证部署、T6 复盘。
- 我完成了什么：
  - 将 Demo 从说明页升级为中文双循环动态控制台。
  - 首屏突出 GPT-Pro × Claude × Codex，以及两个核心循环：Loop 1 方案校验循环、Loop 2 执行验证循环。
  - 增加可点击节点、下一步推进、自动演示、G3 后进入下一轮 010。
  - 点击节点会联动：当前 Agent、动作、产物、审查信号、证据链、提示词。
  - 更新 README、DESIGN.md、预览图，并部署到 GitHub Pages。

- 落盘文件核对（对照产物清单逐条）：

| 清单序号 | 路径 | 是否与清单逐字一致 | 新增/修改 |
|---|---|---|---|
| 1 | DESIGN.md | 是 | 修改 |
| 2 | docs/dev/plans/211-v4-dual-loop-control-room-plan.md | 是 | 新增 |
| 3 | apps/researchloop.html | 是 | 修改 |
| 4 | README.md | 是 | 修改 |
| 5 | assets/researchloop-demo-preview.png | 是 | 修改 |
| 6 | docs/retrospectives/2026-06-20-v4-dual-loop-control-room.md | 是 | 新增 |

- 我遇到的问题 -> 如何解决：
  - 问题 1：README 写入脚本中 Markdown 反引号与 JavaScript 模板字符串冲突。
  - 排查过程：Node REPL 返回 Unexpected token，定位为 Markdown 内联反引号导致模板提前结束。
  - 解决方案：README 使用安全 Markdown 写法，避免脚本冲突。
  - 支撑证据：CX-R211-01（A）README 成功写入并通过必要字段扫描。
  - 问题 2：PowerShell 中文输入导致计划文件出现问号字符。
  - 排查过程：检查计划文件片段发现中文行被替换为问号。
  - 解决方案：改用 Node UTF-8 重写完整 plan。
  - 支撑证据：CX-R211-02（A）manifest 编码扫描为 0。
  - 问题 3：首次 gh-pages push 出现 TLS 握手失败。
  - 排查过程：构建已完成，失败点在远程推送。
  - 解决方案：保留构建目录并重试 push，第二次成功。
  - 支撑证据：CX-R211-06（A）gh-pages 推送成功到 5fa8ecc。

- 与计划的偏差（如有）/ 是否触发回传：
  - 无功能偏差；页面仍为静态公开 Demo，不调用外部 API。
  - 未触发 RESEARCH CONFLICT。

- 测试结果（对照 Test Oracle）：
  - 本地 Playwright / 期望无 pageerror、关键交互可用 / 实际 errors=[]，点击 L1-030 后 agent=Claude signal=BLOCKER，点击 L2-EXEC 后 agent=Codex signal=RISK / PASS。证据：CX-R211-03（A）。
  - G3 回环 / 期望最后节点下一步回到下一轮 010 / 实际 beforeWrap=L2-REVIEW，afterWrap=Round 2 L1-010 / PASS。证据：CX-R211-04（A）。
  - 预览图 / 期望 assets/researchloop-demo-preview.png 更新 / 实际 preview_size=736128 bytes / PASS。证据：CX-R211-05（A）。
  - 扫描 / 期望旧版无关词集合、公开边界、编码疑似命中均为 0 / 实际 old_hits=0，sensitive_hits=0，manifest_mojibake_hits=0 / PASS。证据：CX-R211-02（A）。
  - GitHub Pages HTTP / 期望 200 且包含 V4.1、双循环和三角色 / 实际 status=200，v41=true，dual=true，roles=true，old=false / PASS。证据：CX-R211-07（A）。
  - Live browser / 期望远程页面零错误、点击联动和回环正常 / 实际 errors=[]，loop1Live=Claude/BLOCKER，loop2Live=Codex/RISK，wrapLive=Round 2 L1-010，imgLoaded=true / PASS。证据：CX-R211-08（A）。

- 保留的临时物 / 待清理项：
  - gh-pages 构建临时目录位于系统临时目录，未写入仓库。
  - 无需要提交的临时文件。

## Evidence IDs

- CX-R211-01（A）：README V4.1 内容写入成功，包含 Live Demo、Preview、Quick Start、Privacy Boundary、双循环控制台。
- CX-R211-02（A）：扫描结果 old_hits=0，sensitive_hits=0，manifest_mojibake_hits=0。
- CX-R211-03（A）：本地浏览器点击 Loop 1 与 Loop 2 节点后，详情、证据链、提示词同步切换。
- CX-R211-04（A）：本地 G3 回环测试通过，最终节点下一步进入 Round 2 的 L1-010。
- CX-R211-05（A）：新版预览图生成成功，assets/researchloop-demo-preview.png 大小 736128 bytes。
- CX-R211-06（A）：gh-pages 分支推送成功，远程更新到 5fa8ecc。
- CX-R211-07（A）：GitHub Pages HTTP 200，V4.1 内容已刷新。
- CX-R211-08（A）：live Playwright 核验 errors=[]，图片加载与交互回环均通过。
