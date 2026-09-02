# Recursive Experiential-Working Memory Evolution for Long-Horizon Agent Harnesses

> Spotlight（2 句）：长程任务里，agent 往往受“长历史”拖累，出现状态漂移和技能错配。本文提出用递归记忆演化闭环，把执行失败结构化成可修正的证据，显著提升多模型在超长轨迹任务中的成功率。

## 基本信息
- 论文标题：Recursive Experiential-Working Memory Evolution for Long-Horizon Agent Harnesses
- 作者：Zhaochen Yu, Yingcheng Wu, Zhenfei Yin, Kaiyuan Chen, Zhe Zhao, Mengdi Wang, Shuicheng Yan, Ling Yang
- 作者/机构（如可得）：未在 arXiv 页面披露机构信息
- 发布日期（版本）：2026-08-25（v1）
- 主题标签：`#Agent` `#LongHorizon` `#MetaReasoning` `#RL` `#Self-Improvement`
- 论文链接：[https://arxiv.org/abs/2608.24876v1](https://arxiv.org/abs/2608.24876v1)
- PDF 链接：[https://arxiv.org/pdf/2608.24876](https://arxiv.org/pdf/2608.24876)
- 项目/代码/数据链接：
  - 代码： [https://github.com/Gen-Verse/Recuris](https://github.com/Gen-Verse/Recuris)
  - 数据：未公开
  - 项目主页：未公开

## 核心问题
长任务中的 RSI（Recursive Self-Improvement）和行为编排难点在于：随着交互长度增加，历史上下文过长使得状态跟踪不稳，导致技能选择与执行偏离当前目标，难以持续纠错。

## 方法概要
1. 提出 Recuris 框架，把 Working Memory 与 Experiential Memory 解耦：前者维护任务进展结构，后者存储可复用经验。
2. 设计基于失败证据的执行结构化表示，支持以“哪个记忆组件出错”作为可定位反馈。
3. 引入固定 Meta-Agent，按步骤对证据进行验证门控（validation-gated）的局部更新，形成记忆演化闭环。
4. 用同一套元更新机制替代一次性微调，支持长期交互后逐步提高行为策略。

## 主要贡献
- 给出一种“递归记忆演化”范式，使 agent 能在运行中持续吸收失败证据并修改技能检索逻辑。
- 将长时序任务中的错误定位问题变为可追踪、可局部修复的结构问题。
- 将该机制与现有长任务基准结合，展示了跨模型稳定提升的可迁移路线。

## 关键实验或结果
- 在 4 个长程基准与 10 个主流模型上评测。
- 在 37 个完成的模型-基准组合中，任务成功率提高 35 组。
- GPT-5.6 Sol +17.8 分，Claude Opus 5 +15.6 分；Qwen3.6-27B/35B 在 SkillFlow +16.6/+13.5 分。
- 最长时程任务可达 +32.2 分，常见失败率下降约 80%。

## 适合关注的原因
论文直接回应了“长期代理系统如何不断改进自己”这个核心问题，且结果不仅是单模型点增益，而是体现了“可复用的记忆机制 + 统一训练外循环”路径，具有较强工程和方法迁移价值。

## 局限性或待验证点
- 论文描述的性能优势依赖于 benchmark 设定与评测策略，真实异构产品流程中的稳健性仍需验证。
- 代码开源程度与超参/计算资源开销的细节未在摘要中完全展开，需要结合论文正文确认复现实验边界。
- 在高噪声交互（感知误差、外部工具故障）下的错误传播机制尚未给出充足证据。

## 对后续研究/应用的启发
- 可以将“失败证据→局部记忆更新”的结构迁移到多智能体协作与任务规划器中。
- 在企业级长流程任务中，建议先从“可解释失败归因层”切入，再接入记忆演化模块。
- 对 agent 产品而言，这是把“调参”变“在线学习”最可操作的技术路线之一。

## 适合 Obsidian 快速浏览的中文总结
这是篇能把“长链任务误差难以收敛”的问题变成可迭代记忆更新机制的工作，尤其在 tau-bench/SkillFlow 上有明显大幅收益。

## 标准化研究框架
- **Research question：** 面对长时序、多步骤目标，能否通过可解释的记忆演化机制持续提高 agent 成功率，而不是依赖一次性 prompt/模型更新？
- **Literature：** 相比以往一次性策略优化方法，本框架更强调持续更新的执行-反馈闭环，与 agentic 系统中的 reflective loop 思路一致，但扩展到长时序记忆结构化。
- **Theory：** 长任务成功率下降的主要机制可被建模为“状态表示衰减 + 技能调用误对齐”，而递归记忆更新可通过局部证据消除这两类偏差。
- **Hypotheses：** 1）结构化失败证据能定位关键干预点；2）局部记忆修订能减少错误传播；3）随着交互长度增加，收益非线性上升。
- **Method：** 使用 Recuris 的 Working Memory 与 Experiential Memory 双记忆体系；Meta-Agent 对失败证据进行 validation-gated 的局部更新，并在多个长程基准复测。
- **Data and Analysis：** 以 tau-bench、SkillFlow 等 benchmark 为核心，统计任务成功率、失败类型、提升幅度并进行长度分桶分析。
- **Findings：** 结果支持“记忆演化闭环”对长任务显著有效，尤其在复杂交互长度下优势更明显。
- **Conclusion：** 长程 agent 的可持续改进不应仅靠单次提示工程，递归记忆机制提供了更结构化、可复用的升级路径。
