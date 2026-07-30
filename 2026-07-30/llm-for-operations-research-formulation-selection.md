# Large Language Model for Operations Research Formulation Selection in Multi-Warehouse Inventory Allocation

Spotlight：把 OR 建模决策变成可学习的 selector 问题，用 LLM 进行实例级公式选择，而不依赖单一固定数学规划表述。

- 论文标题：Large Language Model for Operations Research Formulation Selection in Multi-Warehouse Inventory Allocation
- 作者：Jintao Xu, Yingzheng Ma, Jiong Dong, Yongzhi Qi, Jianshen Zhang
- 机构（如可得）：页面未公开
- 发布日期或版本日期：2026-07-28（v1）
- 主题标签：#AI4S #OperationsResearch #InventoryAllocation #OR-formulation #LLM
- 论文链接：[https://arxiv.org/abs/2607.25956v1](https://arxiv.org/abs/2607.25956v1)
- PDF 链接：[https://arxiv.org/pdf/2607.25956v1](https://arxiv.org/pdf/2607.25956v1)
- 项目/代码/数据链接（如可得）：未在摘要页公开

## 核心问题
- 多仓库存储分配常需选择不同 MIP 公式，但“一个公式适配所有实例”在不同需求结构下通常失败。
- 传统规则依赖专家经验，难以根据实时实例特征快速切换模型。
- 研究问题是是否可以让 LLM 学会“实例到公式”的映射，提高可执行 OR 求解质量而非只做文本生成。

## 方法概要
- 构建 OR formulation selection 框架：把每个实例映射到候选公式库中的最适配公式。
- 先用 SFT 进行 schema 学习，建立专家条件的监督 fine-tuning。
- 再用 MIP solver 输出的质量差距构造奖励信号，设计 IPO 偏好与 per-instance metadata。
- 使用 GRPO 在采样响应中学习选择策略，目标直接优化实例级求解质量。

## 主要贡献
- 首次把 OR 表达选择问题系统化为 LLM selector，直接连接求解器反馈闭环。
- 在同一任务上联合使用 SFT+IPO 与 GRPO，展示多阶段优化链路对 OR 性能的收益。
- 将模型输出从“文本答案”转为“策略动作（公式选择）”以匹配实际业务编排。

## 关键实验或结果
- 数据基于 JD.com 的多仓库存分配实例（真实场景规模背景）。
- Hit Ratio@1 从 21.45% 提升到 50.42%，Hit Ratio@2 从 70.47% 提升到 82.31%。
- 相比固定 formulation 和单一选择器，GRPO 显著提升分配准确率约 12.57 个百分点。
- 与 ex-post oracle 的质量差距降低到 4.85 个百分点。

## 适合关注的原因
- 这是典型 AI4S 场景：LLM 不是替代优化器，而是替代人类专家做实例级决策。
- 通过 solver-in-the-loop 的奖励设计，强调结果导向而非语言流畅度，贴近企业生产可用性。
- 可快速复用到仓配、调度、能源、供应链等需要多公式切换的业务。

## 局限性或待验证点
- 论文以单一任务领域为中心，跨行业迁移和小样本场景仍需验证。
- LLM selector 的稳定性受 prompt 与实例编码质量影响，实际部署需要严格版本管理。
- 缺少对求解时延与成本的联合分析，当前指标仍以质量为主。

## 对后续研究/应用的启发
- 可把“公式选择”扩展成多目标（成本/时延/公平性）的联合选择框架。
- 与数字孪生系统结合，构建可解释的决策日志（为何当前实例选该公式）。
- 与强化学习 / MCTS 混合，处理更复杂网络流和动态库存场景。

## 一句 Obsidian 快速浏览总结
一句话：该文将 OR 的选择权从人类经验规则转向 LLM + 求解器反馈闭环，适合把数学规划的工程门槛真正压到业务一线。

## 标准化研究框架
- **Research question：** 在多仓库存分配中，能否通过 LLM selector + 求解器反馈，实现实例级 formulation 的自动化和更高现实求解质量？
- **Literature：** 属于 AI4S 里“LLM 参与决策优化”的分支，区别于纯文本问答，更强调优化任务的控制决策。
- **Theory：** 将 formulation 选择建模为策略学习问题，目标从局部公式评分转向全局外部求解收益最大化。
- **Hypotheses：**
  - Solver-in-the-loop 的偏好优化可明显提升公式选择准确率；
  - GRPO 可超越仅 SFT+IPO 方案；
  - 实例级选择优于固定公式在异构需求下的平均表现。
- **Method：** 构建候选公式库，训练 SFT 及 SFT+IPO 初始化，再用 solver 评价转化的奖励训练 GRPO selector。
- **Data and Analysis：** 使用 JD.com 多仓库存实例（文中给出的数据背景）评估 hit ratio、分配质量差距与 oracle gap 的减少。
- **Findings：** 论文指标显示 GRPO 在命中率和质量上明显改善，且与固定公式基线保持持续领先。
- **Conclusion：** LLM 在 AI4S 场景中可作为“优化编排器”，尤其适合实例驱动且公式族复杂的问题。
