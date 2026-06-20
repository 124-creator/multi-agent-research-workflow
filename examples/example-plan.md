# Plan — 时间序列特征筛选与基线对照（示例 · 脱敏）

> 这是一份真实任务脱敏后的示例，演示 plan 六项怎么填。

## 1. 目标 (Goal)

为某日度时序的 next-day 预测，从候选特征中筛出稳定有效的子集，并确认其相对朴素基线是否真有增益。

## 2. 输入资料 (Inputs)

- `data/anchor_dataset.csv`（已划分 train / dev / test 的锚点数据集）
- `docs/feature_dictionary.md`（候选特征说明）

## 3. 执行步骤 (Steps)

1. 计算 persistence 基线（`y_pred = y_{t-1}`）在 dev 上的 R² / RMSE。
2. 用四法（Pearson、Spearman、灰色关联、稳健显著性检验）联合筛选候选特征。
3. 在 train 上拟合显式回归，在 dev 上做分块交叉验证。
4. 对比筛选后模型与 persistence 基线，记录技巧分（skill score）。

## 4. 成功标准 (Acceptance Criteria)

- 生成 `result/feature_selection_summary.csv`，含每个特征的四法得分。
- dev 分块 CV 的 R² 与 persistence 基线技巧分**同时报告**。
- 明确给出"外生特征是提供解释还是提供短期预测增益"的判断。

## 5. 风险与应对 (Risks & Mitigations)

| 风险 | 影响 | 应对 |
|---|---|---|
| 强惯性导致基线难超 | 误判模型失败 | 报告技巧分而非只看 R²，区分解释力与预测增益 |
| 全样本筛选泄漏 | 高估性能 | 仅用 train 拟合，dev / test 不参与筛选 |

## 6. 当前状态 (Status)

- [x] 已完成
- 备注：结论为"外生因素主要提供解释而非短期预测增益"，已写入复盘。
