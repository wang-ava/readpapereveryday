# ClawGym II: Exploring Black-Box RL on Agent Harness

Spotlight：ClawGym II 的核心价值在于把“在复杂 harness 上做黑盒 RL”从难以扩展的问题变成系统工程问题：通过 sandbox 化隔离和调用轨迹重建，让训练与推理一致。它对可复用代码代理任务很关键，因为很多真实系统都在模型边界可观测但环境内部不可插拔的条件下运行。

## 论文信息
- 论文标题：ClawGym II: Exploring Black-Box RL on Agent Harness
- 作者（机构）：Huatong Song、Fei Bai、Ming Yang、Renyuan Li、Jia Deng 等（机构未在 arXiv 元信息中明确给出）
- 发布日期：2026-08-17（v1）
- 主题标签：`#Agent` `#RL` `#LLM` `#Harness` `#BlackBoxRL`
- 论文链接：[https://arxiv.org/abs/2608.16798v1](https://arxiv.org/abs/2608.16798v1)
- PDF 链接：[https://arxiv.org/pdf/2608.16798v1](https://arxiv.org/pdf/2608.16798v1)
- 项目/代码/数据链接（如可得）：
  - 相关项目生态（含 benchmark）：[https://github.com/ClawGym](https://github.com/ClawGym)

## 论文内容
- 核心问题：当 agent harness 复杂且内部执行不可直接调参时，如何对通用代理进行稳定、可扩展的强化学习优化，而不是依赖白盒重构。
- 方法概要：构建沙箱化执行基础设施，在任务与 harness 周期内做大规模并发 rollout；通过 serving proxy 截获模型调用并重建多轮 prefix tree；在树结构上同时应用 PPO 与 GRPO；并引入 mix-harness 机制统一优化多个 harness。
- 主要贡献：
  - 给出稳定的黑盒代理优化范式，解决调用边界不可见导致的训练噪声和状态重建问题。
  - 利用 prefix-tree 表征复用调用轨迹，减少浪费并保持训练-推理一致性。
  - 在异构 harness 场景下实现统一训练，缓解单一工具栈过拟合风险。
- 关键实验或结果：
  - 在 ClawGym-Bench 上，Qwen3-30A3B 经黑盒 RL 后 Pass@1 提升 9.98（OpenClaw）和 14.81（Claude Code）分。
  - 在 200–400 次优化步内保持稳定，不易出现训练崩溃。
  - 在 JobBench、OfficeQA 上也观察到持续增益，说明方法对复杂任务具备一定迁移性。
- 适合关注的原因：
  - 这类方法贴近真实“工具代理”部署场景，能够直接回应如何在不改动工具内部实现的前提下继续提升代理表现。
  - 统一优化与多-harness 机制对未来企业级智能体平台具有明显工程价值。
- 局限性或待验证点：
  - 论文未给出全部代码版本与复现实验细节，工程复现成本仍高。
  - 在超高成本或高延迟的外部工具链中，prefix tree 和大规模并发的计算成本可能成为瓶颈。
  - 论文以部分 benchmark 为主，真实企业工作流是否保持同等收益仍需验证。
- 对后续研究/应用的启发：
  - 可借鉴其“服务代理 + 调用轨迹树”思想，为 AI coding assistant、客服 agent、知识搜索 agent 建立统一优化后端。
  - 值得与可验证执行（verifier）和安全策略联合，形成带合规边界的黑盒增强闭环。
- Obsidian 快速浏览一句总结：**ClawGym II 显示 LLM 代理在不透明工具生态里也能通过轨迹级重建实现规模化优化。**

## 标准化研究框架
**Research question：** 在无法访问模型内部实现或环境内部细节的情况下，是否能通过调用轨迹重建和 harness 化训练机制稳定提升 agent 性能？

**Literature：** 现有工作多假设代理内部可控或环境可白盒优化，本方法更接近工业场景；在 agent harness 方向与黑盒优化的交集上具有较强实用性。

**Theory：** 可将黑盒代理优化看作“在工具边界观察到的状态序列”上做序列决策学习，prefix tree 使多轮行为可压缩和复用，使离散控制更可学习。

**Hypotheses：**  
- H1：将多轮调用重建为树结构能减少噪声并提高样本利用率。  
- H2：混合 harness 训练提高泛化到不同执行系统的稳定性。  
- H3：PPO 与 GRPO 的任务适配组合可在不同难度任务上维持更高稳定性。

**Method：** 搭建沙箱并发执行环境；建立模型边界代理捕获调用；将调用序列转为 prefix tree；在树上优化策略（critic/PPO 与 GRPO）；将同一策略在多个 harness 上联合训练验证。

**Data and Analysis：** 使用 ClawGym-Bench 为主的长链任务和 JobBench、OfficeQA 的更复杂基准；比较 open-calls 与 baseline 的 Pass@1、稳定性与优化步数曲线。

**Findings：** 论文报告的提升幅度较大且优化过程稳定，支持“黑盒可训练性”在代理优化中的可行性。

**Conclusion：** ClawGym II 的结论提示：在可观测边界受限场景，关键不在于重构内部模型，而在于设计可学习的调用结构与统一训练协议。
