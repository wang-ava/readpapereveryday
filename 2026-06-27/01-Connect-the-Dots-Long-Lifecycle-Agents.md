# Connect the Dots: Training LLMs for Long-Lifecycle Agents with Cross-Domain Generalization Via Reinforcement Learning

这篇文章把“长期部署代理人”的核心能力 formalize 成一个可训练的 meta-skill：agent 不只在单次任务上做得好，而要通过长序列交互不断更新环境线索，实现跨任务迁移。对想落地自治服务、研发协同体、工具链编排器的人来说，这类“会学会在部署中成长”的训练范式很值得关注。

- **论文标题**：Connect the Dots: Training LLMs for Long-Lifecycle Agents with Cross-Domain Generalization Via Reinforcement Learning
- **作者/机构（如可得）**：Yanxi Chen, Weijie Shi, Yuexiang Xie, Boyi Hu, Yaliang Li, Bolin Ding, Jingren Zhou（机构未在 arXiv 页面明确列出）
- **发布日期/版本日期**：2026-06-18（v1）
- **主题标签**：#LLM #Agent #ReinforcementLearning #LongLifecycle #CrossDomain
- **论文链接**：<https://arxiv.org/abs/2606.20002v1>
- **PDF 链接**：<https://arxiv.org/pdf/2606.20002v1>
- **项目/代码/数据链接（如可得）**：实现代码：<https://github.com/agentscope-ai/Trinity-RFT/tree/research/cod/examples/research_cod>；其余数据与 benchmark 在摘要层面未公开完整清单

- **核心问题**：传统评测更多关注“单任务即时表现”，很少覆盖 agent 在真实环境中的长期运行机制。该文面向长期生命周期部署，核心问题是如何训练 LLM 具备 *Connect the Dots（CoD）*：在多任务序列中通过自我探索与上下文更新逐步提升后续能力。

- **方法概要**：
  1. 明确定义 CoD，并区分“solve-task episode”与“update-context episode”的双阶段部署循环。
  2. 构建可端到端长轨迹强化学习（long rollout RL）框架，核心为持续交互中上下文迭代更新。
  3. 实验设计上同步构建任务和环境，专门激励 CoD 而非特定领域能力；配套 GRPO 风格的信用分配策略。
  4. 同时验证训练自由（training-free）与训练增强（RL-based）两类 setting 下的 agent 表现，重点比较跨域外推能力。

- **主要贡献**：
  1. 提出可复用的 CoD 任务范式，将长期记忆更新与任务解决耦合为统一训练目标。
  2. 给出长滚动轨迹 RL 的算法与基础设施框架，覆盖部署时上下文更新的关键链路。
  3. 用同一训练框架测试跨域和 OOD 一致性，推动 agent 训练从“短视任务解答”走向“跨时间学习能力”。

- **关键实验或结果**：
  - 实验显示 CoD 训练显著提升 long-horizon 任务中的持续表现，并在训练域内跨任务、跨域以及从 CoD 到 Ralph-loop 的设置里展现外推潜力。
  - 论文强调该范式在评估层面能更好区分“会做当前任务”与“会在长期运行中改善”。

- **适合关注的原因**：
  1. 当前 agent 应用普遍面临“上线即失效”问题，本篇直接针对这个问题给出训练视角。
  2. 连接了训练与部署链路，减少研究方法与工程部署之间的鸿沟。
  3. 对企业级 agent（客服、研发助手、运维自动化）提供了更真实的成长目标定义。

- **局限性或待验证点**：
  1. CoD 基线和任务集实现细节未在摘要里完全展开，复现门槛较高。
  2. 长 rollout RL 对算力和轨迹长度敏感，规模化成本仍是关键约束。
  3. 不同部署场景中的安全边界（污染、漂移利用）需要更多评估。

- **对后续研究/应用的启发**：
  可借鉴“解耦 solve 与 update-context”的框架，把 agent 部署成循环学习系统：例如把问题诊断、策略更新、知识缓存更新分离，以便在生产系统中监控并独立优化。

- **Obsidian 快速浏览的一句总结**：本篇提供了从“会一次答题”到“会持续成长”的训练路线图，是构建长期自治 agent 的关键里程碑。

## 标准化研究框架
- **Research question：** 如何让 LLM agent 在连续多任务部署中，通过交互生成的上下文更新实现跨任务、跨域持续改进？
- **Literature：** 与现有单任务 RLHF / task-specific RL 对比，本文把研究焦点从单 episode 决策转移到生命周期学习能力建模。
- **Theory：** 假设长时上下文更新本身可被显式建模为策略的一部分，且可通过 credit assignment 在长轨迹中被优化。
- **Hypotheses：** 如果 agent 在部署中能够正确区分 solve 与 update-context 两类行为，则其后续任务成功率与跨域泛化会显著提升。
- **Method：** 设计 CoD 框架，构造含 solve/update-context 的 rollout 轨迹；应用 GRPO 风格 RL 与专用评估任务测量长期能力。
- **Data and Analysis：** 使用作者自建任务/环境评估跨域与 OOD 情况，比较训练前后 agent 的持续表现及迁移曲线。
- **Findings：** CoD 训练增强了长期性能和迁移能力，并在不同设置下显示出更好的外推趋势。
- **Conclusion：** 在非社会科学实证语境中，本文可解释为“可持续成长的 agent 控制策略学习范式”；其价值在于把 agent 训练目标升级为长期闭环。
