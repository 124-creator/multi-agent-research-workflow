# ResearchLoop V4 Demo top-tier upgrade retrospective

### 复盘块 · 任务 T1-T6 · V4 Demo 页面升级与 GitHub Pages 发布 · 2026-06-20

- 对应 plan 任务 / 路线部分：RL-V4-DEMO-210 · T1 设计契约、T2 Demo 实现、T3 README、T4 预览图、T5 验证部署、T6 复盘。
- 我完成了什么：
  - 重写 apps/researchloop.html 为单文件静态交互 Demo，包含顶尖视觉首屏、Task Lab、Flow Playback、Gate Simulator、Evidence Ledger、Case Study Replay、Prompt Kit、内联 favicon。
  - 重写 README.md，修复编码显示风险，加入 Live Demo、Preview、Quick Start、Privacy Boundary、协议地图和仓库结构。
  - 生成 assets/researchloop-demo-preview.png 作为 README 和 GitHub 展示预览图。
  - 写入 DESIGN.md 和 approved plan，保留设计源事实与 Test Oracle。
  - force-push gh-pages 并远程验证 https://124-creator.github.io/ResearchLoop/ 已刷新为新页面。

- 落盘文件核对（对照产物清单逐条）：

| 清单序号 | 路径 | 是否与清单逐字一致 | 新增/修改 |
|---|---|---|---|
| 1 | DESIGN.md | 是 | 新增 |
| 2 | docs/dev/plans/210-v4-demo-top-tier-upgrade-plan.md | 是 | 新增 |
| 3 | apps/researchloop.html | 是 | 修改 |
| 4 | README.md | 是 | 修改 |
| 5 | assets/researchloop-demo-preview.png | 是 | 新增 |
| 6 | docs/retrospectives/2026-06-20-v4-demo-top-tier-upgrade.md | 是 | 新增 |

- 我遇到的问题 -> 如何解决：
  - 问题 1：第一次尝试通过超长 PowerShell inline 命令写 HTML 时触发 Windows 命令长度限制。
  - 排查过程：命令返回文件名或扩展名太长，说明不是 HTML 内容错误，而是 shell 传参长度问题。
  - 解决方案：改用 Node REPL 直接以 UTF-8 写入文件，避免 shell 命令长度限制。
  - 支撑证据：CX-R210-01（A）apps/researchloop.html 成功写入并通过本地浏览器验证。
  - 问题 2：远程浏览器最初出现 favicon 404。
  - 排查过程：live 页面内容正确但控制台出现 404；第一次插入 favicon 的脚本因为标题匹配不稳定未实际写入。
  - 解决方案：改为在 title 标签前插入内联 SVG favicon，重新本地验证并重新部署 gh-pages。
  - 支撑证据：CX-R210-05（A）最终 live browser verification errors=[]，favicon=true。
  - 问题 3：GitHub Pages CDN 短暂保留上一版内容。
  - 排查过程：HTTP 已 200，但 favicon=false；使用 cache-bust query 多次重试后刷新到 favicon=true。
  - 解决方案：等待 Pages 刷新并再次核验。
  - 支撑证据：CX-R210-04（A）try=2 status=200 hero=true favicon=true old=false bytes=61046。

- 与计划的偏差（如有）/ 是否触发回传：
  - 无功能偏差；为了消除远程 favicon 404，增加了内联 SVG favicon，仍属于 apps/researchloop.html 范围。
  - 未触发 RESEARCH CONFLICT。

- 测试结果（对照 Test Oracle）：
  - 本地 Playwright / 期望无 pageerror、关键模块存在、流程图加载 / 实际 errors=[]，titleOk=true，labels=true，imgLoaded=true，stepActive=040 / PASS。证据：CX-R210-01（A）。
  - 预览图生成 / 期望 assets/researchloop-demo-preview.png 存在 / 实际 preview_size=460095 bytes / PASS。证据：CX-R210-02（A）。
  - 旧词与敏感信息扫描 / 期望 old_hits=0、sensitive_hits=0、mojibake_hits=0 / 实际全部为 0；README required fields Live Demo、Preview、Quick Start、Privacy Boundary 全部 true / PASS。证据：CX-R210-03（A）。
  - GitHub Pages HTTP / 期望 200 且新 hero 内容存在 / 实际 status=200，hero=true，favicon=true，old=false，bytes=61046 / PASS。证据：CX-R210-04（A）。
  - Live browser / 期望控制台零错误、图片加载、交互可用 / 实际 errors=[]，titleOk=true，favicon=true，labels=true，stepActive=040，caseHeading=Portfolio Demo Delivery，imgLoaded=true，imgWidth=1086，oldTerms=false / PASS。证据：CX-R210-05（A）。

- 保留的临时物 / 待清理项：
  - gh-pages 构建临时目录位于系统临时目录，未写入仓库。
  - 无需要提交的临时文件。

## Evidence IDs

- CX-R210-01（A）：本地浏览器验证，apps/researchloop.html 无 pageerror/console error，关键模块与交互存在，流程图 naturalWidth=1086。
- CX-R210-02（A）：README 预览图 assets/researchloop-demo-preview.png 生成成功，大小 460095 bytes。
- CX-R210-03（A）：仓库公开文本扫描 old_hits=0、sensitive_hits=0；manifest 文本 mojibake_hits=0；README 必要字段全部存在。
- CX-R210-04（A）：GitHub Pages 远程 HTTP 200，hero=true，favicon=true，old=false，bytes=61046。
- CX-R210-05（A）：live Playwright 验证 errors=[]，图片加载、交互、关键模块、旧词检查全部通过。
