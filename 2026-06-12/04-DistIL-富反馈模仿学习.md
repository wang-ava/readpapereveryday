# Reinforcement Learning from Rich Feedback with Distributional DAgger

这篇论文把“只看最终正确/不正确”反馈升级为“富反馈序列”建模，把 RLVR 的稀疏评估瓶颈转为可利用的分布式模仿学习问题。

- **论文标题**：Reinforcement Learning from Rich Feedback with Distributional DAgger
- **作者/机构**：Rishabh Agrawal，Jacob Fein-Ashley，Paria Rashidinejad；项目提交方为 University of Southern California
- **发布日期/版本日期**：2026-06-03（arXiv:2606.05152，Hugging Face page 显示 Published on Jun 3）
- **主题标签**：#Agent #ReinforcementLearning #DistIL #DAgger #LLM
- **论文链接**：[https://arxiv.org/abs/2606.05152](https://arxiv.org/abs/2606.05152)
- **PDF 链接**：[https://arxiv.org/pdf/2606.05152.pdf](https://arxiv.org/pdf/2606.05152.pdf)
- **项目/代码/数据链接（如可得）**：[https://rishabh-1086.github.io](https://rishabh-1086.github.io)（项目页）；Hugging Face 页面展示 GitHub 资源（按钮可在原页继续展开）
- **核心问题**：传统 RLVR 通常只依据最终结果的单比特奖励，无法利用执行轨迹、工具输出、人工纠错等富信号，导致优化方向不精确。
- **方法概要**：
  1. 将问题重构为 distributional DAgger：学习学生策略与专家分布之间的偏差；
  2. 使用 forward cross-entropy 目标进行黑盒专家的分布式 imitation；
  3. 基于理论上可证单调改进的策略更新证明，构建更稳定的政策迭代机制。
- **主要贡献**：
  1. 提出 DistIL（distributional DAgger）作为富反馈训练范式；
  2. 纠正 RLVR 在富反馈场景下的退化风险；
  3. 给出单调改进和 regret 相关理论基础。
- **关键实验或结果**：在科学推理、代码、数学推理等任务上，DistIL 对比 RLVR 与传统自蒸馏/自我提升策略显示更优，Pass@N 改善显著。
- **适合关注的原因**：
  1. 直接对应当前 agent 工具链中常见的富上下文、长链路反馈场景；
  2. 理论与实验都给出较清楚的改进方向；
  3. 可迁移到 reasoning agent 的策略蒸馏与持续学习。
- **局限性或待验证点**：
  1. 富反馈数据质量依赖显著，分布偏移可能影响专家信号稳定性；
  2. 与多模态工具调用任务中的反馈结构匹配仍需测试；
  3. 公开实验主要覆盖文本推理领域，工业任务验证尚不足。
- **对后续研究/应用的启发**：可作为 agent 的“策略蒸馏阶段”替代传统 reward-only 训练，构建更强的轨迹学习和纠错反馈闭环。
- **Obsidian 快速浏览一句总结**：DistIL 让 agent 学得更像“看反馈做决策”，而不是“只靠最终正确率赌博”。

## 标准化研究框架
- **Research question：** 如何把丰富反馈（轨迹/工具/纠错）转成可训练策略信号，减少 RLVR 的奖励信息损失？
- **Literature：** 与 RLVR、imitation learning、DAgger、agent self-distillation 工作衔接，差异点在于 reward 分布化处理。
- **Theory：** 利用 forward cross-entropy 的分布式目标与最优化界，构造策略改进路径并减少反向 KL 的局限。
- **Hypotheses：** 引入 rich feedback 时，分布式 imitation 能提升策略稳定性与样本效率，尤其在多任务推理场景。
- **Method：** 将单比特 reward 场景扩展为富反馈 DAgger：记录状态轨迹、执行反馈并拟合专家分布，采用 forward CE 进行更新。
- **Data and Analysis：** 在科学推理、代码和数学推理基准上比较 DistIL 与 RLVR、RLDistill 等基线；观察 Pass@N 等任务指标。
- **Findings：** DistIL 在多任务上更优，且在理论上具备单调改进与 regret 上界支撑。
- **Conclusion：** 这是把 rich feedback 落地到 agent 训练的一条可复用路径，但需在真实 tool-use 场景下扩展验证。
