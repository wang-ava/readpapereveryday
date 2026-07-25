# OpenForgeRL: Train Harness-native Agents in Any Environment

Spotlight：这篇工作把“agent 在复杂 harness 上能做但很难训练”的矛盾直接打通，能在单个统一框架里训练与部署闭环。若你要做生产级 AI Agent，它更偏“可落地工程方向”，而不仅是新算法概念验证。

- 论文标题：OpenForgeRL: Train Harness-native Agents in Any Environment
- 作者：Xiao Yu, Baolin Peng, Ruize Xu, Hao Zou, Qianhui Wu, Hao Cheng, Wenlin Yao, Nikhil Singh, Zhou Yu, Jianfeng Gao
- 机构（如可得）：未在该版本 arXiv 页面直接给出机构信息
- 发布日期或版本日期：2026-07-23（v1）
- 主题标签：#LLM #Agent #ReinforcementLearning #Agentic
- 论文链接：[https://arxiv.org/abs/2607.21557v1](https://arxiv.org/abs/2607.21557v1)
- PDF 链接：[https://arxiv.org/pdf/2607.21557v1](https://arxiv.org/pdf/2607.21557v1)
- 项目/代码/数据链接（如可得）：论文称为 open-source，但本文版本未提供稳定可直接检索链接；建议关注后续版本的仓库更新与发布说明

## 核心问题
- 复杂推理 harness（如 Codex、Claude Code 等）虽强大，但无法被常规 SFT/RL 框架原生训练，导致“能做但难训”。
- 如何在不重写现有 harness 的前提下，把真实部署行为转化为可训练样本并进行规模化优化？
- harness 选择与训练策略如何影响 agent 的长链路鲁棒性、工具使用覆盖率和错误恢复能力？

## 方法概要
- 设计轻量 proxy，把 harness 的模型调用转接为标准 RL 训练可记录数据。
- 使用 rollout-level 记录与容器化执行（Kubernetes orchestrator）解耦训练和推理过程。
- 在统一 RL stack（如 veRL 示例）中训练 agent policy，覆盖工具/多进程/长对话交互流程。
- 在多类环境中验证，含 tool/claw、GUI 浏览器与 computer-use 类场景。

## 主要贡献
- 给出 harness-native Agent 的可行训练范式，解决长期困扰 agent 开发的工程落地瓶颈。
- 提供跨环境可复用框架，支持“以真实部署环境为目标”而非仅靠静态 simulator 的训练。
- 通过实验比较呈现多种 harness 的可学性差异和 RL 对行为质量的显著影响。

## 关键实验或结果
- OpenForgeClaw 在 ClawEval 的 pass^3 为 31.7，pass@3 为 55.9，在 QwenClawBench 为 33.7。
- OpenForgeGUI 在 OSWorld-Verified 为 37.7，在 Online-Mind2Web 为 63.0，在 WebVoyager 为 72.3。
- 与同量级开源基线相比，部分 benchmark 接近或超过更大模型，显示训练策略对“真实 harness 适配能力”有关键作用。

## 适合关注的原因
- 对希望把 LLM agent 从 demo 推向可验证系统的团队意义直接且强：训练可控、可复现、可度量。
- 对比传统的 “in-context prompt 化”方法，该框架更接近工程团队可长期迭代的 MLOps 流。
- 指向“多 harness 协同、任务分发、行为稳健性”这类实际投入最重的难题。

## 局限性或待验证点
- 开源链接未完整公开，当前阶段复现实验门槛仍高于理想。
- 当前结果更偏近端 benchmark，而非大规模真实业务闭环（如高频变更 API、复杂权限策略环境）。
- “error recovery”仍被作者指出为明显短板，说明仍需更强的不确定性控制与回滚机制。

## 对后续研究/应用的启发
- 可将本框架和组织的工具治理策略（日志、审核、自动重试）对齐，形成合规可追责的 agent pipeline。
- 后续研究可进一步把 harness 选择策略、奖励设计和成本约束统一建模，避免在不同平台间重复调参。
- 企业场景下建议把它当作“低速迭代期”控制器：先做局部任务闭环稳态，再扩展大规模任务分发。

## 一句 Obsidian 快速浏览总结
一句话：OpenForgeRL 的重点不是新型推理模型，而是把能在复杂 harness 上执行的 agent 变成可训练、可量化并可持续优化的系统单元。

## 标准化研究框架
- **Research question：** 在真实 harness 上运行的 AI agent 如何实现端到端训练，而不牺牲部署一致性与工具交互复杂性？
- **Literature：** 承接了 Agentic RL、tool-use benchmark、RLHF/行为蒸馏等方向，但弥补了“训练环节与推理环境解耦不足”的工程短板。
- **Theory：** 将 harness 调用视为可采样的环境交互过程，核心在于把可观测行为与内部状态转写为 RL 的马尔可夫决策信号。
- **Hypotheses：** 若训练数据来自真实 harness 行为轨迹且包含动作后果监督，agent 的可靠性与任务完成率应显著提高。
- **Method：** 通过 proxy 记录 state/action/feedback triplet，结合容器化 rollout，使用标准 RL 框架训练并评估多环境泛化。
- **Data and Analysis：** 采集来自多类 harness 任务轨迹，在 ClawEval、QwenClawBench、OSWorld-Verified、Online-Mind2Web、WebVoyager 上按 pass、pass^3、pass@k 等指标比较不同 harness 与模型配置。
- **Findings：** open-source harness-native 训练在多项 benchmark 上表现领先，显示该范式对交互复杂任务有明显优势，但在故障恢复方面仍不足。
- **Conclusion：** 本研究把“AI agent 可训练性”从理论概念推进到工程主线，后续价值在于将该闭环扩展到高成本生产任务与安全约束更强的环境。
