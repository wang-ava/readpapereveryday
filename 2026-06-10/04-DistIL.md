# Reinforcement Learning from Rich Feedback with Distributional DAgger

这篇文章把 RLVR 的二值反馈局限改成分布式、逐步信用分配，核心贡献在于“更丰富反馈下的模仿学习可单调改善策略”，很适合观察下一代 Reasoning Agent 的优化范式变化。 

## 基本信息

- 论文标题：Reinforcement Learning from Rich Feedback with Distributional DAgger
- 作者/机构（如可得）：Rishabh Agrawal；Jacob Fein-Ashley；Paria Rashidinejad（项目页显示作者机构为 University of Southern California）
- 发布日期或版本日期：2026-06-03（v1）；2026-06-05（v2）
- 主题标签：#Reasoning #LLM #DistributionalDAgger #RLVR #AgentTraining
- 论文链接：https://arxiv.org/abs/2606.05152
- PDF 链接：https://arxiv.org/pdf/2606.05152
- 项目/代码/数据链接（如可得）：
  - 项目页：https://rishabh-1086.github.io/project-distIL/
  - 代码：https://github.com/rishabh-1086/distIL
  - 数据：论文内报告科学推理、编码、数学任务上的 benchmark（如 SciKnowEval、LAB 相关），未见单独公开统一数据仓库链接

## 核心问题

当前 reasoning model 的常规 RLVR 仅对最终正确与否赋值，难以利用执行过程中的复杂反馈。问题是：如何把执行过程中的 token/步骤级反馈转化为稳定学习信号，并避免更新过程出现“表面改善但最终变差”的情况？

## 方法概要

作者提出 DistIL（Distributional DAgger）：

- 用教师分布（由反馈构造）（由反馈构造）与学生分布做前向交叉熵对齐；
- 在序列级别累计未来反馈差异，实现“future-credit propagation”，让早期决策也接收后续失误信息；
- 给出单调策略改进与 regret 上界的理论论证。 

## 主要贡献

- 将 DAgger 从单步标注范式扩展到 distributional 反馈场景；
- 用可传播的未来反馈项解释为什么 token 级 dense supervision 能带来更稳定优化；
- 证明部分算法在理论上不保证单调改善，而 DistIL 满足单调策略改进条件。

## 关键实验或结果

- 在科学推理（SciKnowEval-L3）中，DistIL 相比 RLVR/SDPO/OPSD 有更高的 avg@16 与 pass 指标；
- 在编程（LCB v6）和数学（AIME25/AIME24 等）任务也有一致优势；
- 在多个 Qwen3 配置上呈现更稳定学习曲线，减少后期发散。 

## 适合关注的原因

对于 LLM Agent，尤其是工具调用、多轮推理场景，很多反馈天然是非二元、分层和延迟的。DistIL 给出一种可直接接入的训练范式，兼顾可证明性和工程可复用性。 

## 局限性或待验证点

- 论文当前验证主要在 benchmark/离线评测中，真实在线系统中的高成本反馈噪声模型仍待验证；
- 需额外设计教师反馈分布估计器，反馈质量不足会放大偏差；
- 在超长轨迹或工具交互链上，复杂度和方差控制仍是关键。

## 对后续研究/应用的启发

- 可将 DistIL 用作“训练后期稳定器”：当策略接近收敛时，通过分布反馈避免倒退；
- 对 multi-turn coding/science agent 可尝试与检索器、执行日志、测试输出联合构造 richer feedback。

## Obsidian 快速浏览总结

一句话：DistIL 是把“有结构反馈”转进 DAgger 的版本，适合把 RLVR 从一次性正确率指标升级到持续可控的策略改进机制。

## 标准化研究框架

**Research question：** 在有富反馈信号时，如何设计 DAgger 型训练使策略更新既利用全轨迹信息又能保证不反向退化？

**Literature：** 相关流派包括 RLVR、self-distillation、SFT+policy optimization。与以往二元奖励相比，本论文聚焦 feedback-rich trajectory 的结构化利用。 

**Theory：** 可视为对策略更新过程的单调改进条件刻画：通过 forward cross-entropy 构造比 reverse-KL 等更稳健的更新方向，不直接对应社会科学中的假设检验。 

**Hypotheses：** 等价于：在同等模型容量下，DistIL 的 future-credit 项可提高长期 token 与任务级性能，且比反向散度目标更不易“短视优化”导致退化。 

**Method：** 定义教师分布（由反馈构造）（基于 rich feedback）与学生分布之间的 forward cross-entropy，并在 rollout 序列上累积未来差异项；在科学推理/编程/数学任务上做统一评测。 

**Data and Analysis：** 数据基于 SciKnowEval、LCB、AIME 族任务等公开 benchmark；分析关注 avg@k、pass@k、收益稳定性（曲线抖动、收敛速度）与退化情况。 

**Findings：** DistIL 在多类任务上带来持续优势，且在后期学习阶段表现更平稳，支持“丰富反馈下更高可用性”。 

**Conclusion：** 对 agent 训练而言，该方法将“结果是否正确”升级为“过程如何指导学习”，适合作为下一代在线/离线混合优化核心；但真实系统还需验证反馈构造与成本权衡。 
