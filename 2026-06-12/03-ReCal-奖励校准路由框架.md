# ReCal: Reward Calibration for RL-based LLM Routing

ReCal 的核心价值在于把“单一标量奖励”导致的 routing 偏差问题显式建模为分解和归一化问题，解决异构任务下代理路由奖励失真。

- **论文标题**：ReCal: Reward Calibration for RL-based LLM Routing
- **作者/机构**：Qihang Yu，Hanwen Tong，Zhengqi Zhang，Bo Zheng，Feng Wei，Shengyu Zhang，Zemin Liu，Fei Wu；机构信息未在当前可抓取条目中逐项展开
- **发布日期/版本日期**：2026-06-10（arXiv:2606.12479，Date: Wed Jun 10 06:59:36 2026）
- **主题标签**：#LLM #LLM-Routing #RewardModel #ReinforcementLearning #Agent
- **论文链接**：[https://arxiv.org/abs/2606.12479](https://arxiv.org/abs/2606.12479)
- **PDF 链接**：[https://arxiv.org/pdf/2606.12479.pdf](https://arxiv.org/pdf/2606.12479.pdf)
- **项目/代码/数据链接（如可得）**：[https://anonymous.4open.science/r/ReCal](https://anonymous.4open.science/r/ReCal)
- **核心问题**：不同任务和实例中 reward 分布差异巨大，直接把 correctness/format 等目标压缩到单一标量 reward，会带来模糊 credit assignment 与优化偏差，影响路由稳定性。
- **方法概要**：
  1. 用分层奖励分解取代单一聚合目标；
  2. 对每个子目标采用 component-wise advantage；
  3. 引入分布感知优化，使用 variance-aware reweighting 和 per-dataset normalization 降低实例间方差影响。
- **主要贡献**：
  1. 明确提出 ReCal 框架并将“奖励校准”作为路由稳态训练约束；
  2. 解决 routing 中的 reward 偏置导致的任务偏好失真问题；
  3. 在 7 个数据集上验证性能提升和训练稳定性。
- **关键实验或结果**：实验显示 ReCal 在 7 个数据集上较 baseline 提升路由性能，且训练更稳定，尤其对异构任务下的 reward 方差鲁棒性更优。
- **适合关注的原因**：
  1. 对多模型路由服务（cost-aware routing、quality-aware routing）可直接借鉴；
  2. 与 agent 决策链路兼容，能降低“高 reward 但质量不升”现象；
  3. 有清晰可执行的 reward 标准化公式。
- **局限性或待验证点**：
  1. 校准收益在不同任务族的长期分布漂移下是否稳定有待更多验证；
  2. 公开实验细节较少，线上真实流量评估仍需补充；
  3. 对极端稀疏/重尾奖励任务的鲁棒性未充分展开。
- **对后续研究/应用的启发**：可将 ReCal 扩展到“工具选择 + 模型路由 + 预算约束”的联合控制器，构建更可信的自动化推理平台。
- **Obsidian 快速浏览一句总结**：ReCal 的关键点是让路由奖励更“可解释、更稳定”，从而让 LLM 代理做得更准、更稳。

## 标准化研究框架
- **Research question：** 在异构任务和非平稳奖励环境中，如何降低 RL-based LLM routing 的 reward 偏差并提升选择稳定性？
- **Literature：** 与多路由 LLM、奖励建模、policy optimization 等相关；与“单一标量 reward”范式相比，强调 reward 结构化建模。
- **Theory：** 对复杂目标进行分量化后，通过方差感知归一化降低训练噪声，实现更一致的策略更新。
- **Hypotheses：** reward 的分层分解和方差校准可减少样本偏见，提高 routing 在多任务下的泛化与稳定性。
- **Method：** 构建 ReCal 框架，分层优势计算 + 分布校准优化；并在多个数据集上比较 baseline 与改进版。
- **Data and Analysis：** 在 7 个公开数据集上进行训练对比；关注 routing 性能与训练稳定性指标。
- **Findings：** 分层+校准对复杂任务 routing 更有利，能在保持收益的同时降低优化偏移。
- **Conclusion：** ReCal 为 LLM routing 提供了可复用的 reward 工程范式，但需补充跨 domain 长期在线验证。
