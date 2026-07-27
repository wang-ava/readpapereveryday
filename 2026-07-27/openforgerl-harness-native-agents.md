# OpenForgeRL: Train Harness-native Agents in Any Environment

Spotlight：OpenForgeRL 在“真实部署 harness 很难端到端训练”这件事上给出可落地解法，把模型调用、rollout 记录和 RL 学习绑成统一闭环。若你在评估可上线的 Agent 系统，这篇论文是把工程问题结构化成可训练问题的高价值模板。

- 论文标题：OpenForgeRL: Train Harness-native Agents in Any Environment
- 作者：Xiao Yu, Baolin Peng, Ruize Xu, Hao Zou, Qianhui Wu, Hao Cheng, Wenlin Yao, Nikhil Singh, Zhou Yu, Jianfeng Gao
- 机构（如可得）：未在该版本 arXiv 页面直接给出机构信息
- 发布日期或版本日期：2026-07-23（v1） / 2026-07-24（v2）
- 主题标签：#LLM #Agent #ReinforcementLearning #Harness #RLHF
- 论文链接：[https://arxiv.org/abs/2607.21557v1](https://arxiv.org/abs/2607.21557v1)
- PDF 链接：[https://arxiv.org/pdf/2607.21557v1](https://arxiv.org/pdf/2607.21557v1)
- 项目/代码/数据链接（如可得）：论文注明为开源框架（open-source）；当前页面未提供可直接引用的公开仓库链接，待后续版本更新

## 核心问题
- 复杂 AI agent 在复杂 harness（如 Claude Code、Codex、OpenClaw）中表现强，但 SFT/RL 框架很难直接接入该状态化、长时序、异步的推理与工具调用循环。
- 如何在不破坏原有工具能力的前提下，把 harness 的推理行为转写为可被标准强化学习栈训练的数据流？
- 哪些 harness 的难度差异最大，RL 的收益点在哪里（比如工具覆盖率、回滚能力、自验证）？

## 方法概要
- 设计 lightweight proxy：拦截 harness 的模型调用与外部交互事件，并将其结构化为训练可采样的数据。
- 引入 Kubernetes 编排：每个 rollout 在独立远端容器执行，隔离上下文与状态，兼容多环境并行。
- 使用标准 RL 工具链（如 veRL）直接对齐训练目标，避免为每个 harness 编写专有训练接口。
- 在多种环境上统一评估：ClawEval、QwenClawBench、OSWorld-Verified、Online-Mind2Web、WebVoyager。

## 主要贡献
- 明确给出“harness-native agent 可端到端训练”的系统化方法。
- 证明训练与推理解耦并保留部署一致性可行，有效提升多平台稳定性。
- 提供可复用的框架视角：harness 接入、日志化、容器化训练、平台级可扩展性。

## 关键实验或结果
- 论文报告 OpenForgeClaw 在 ClawEval/ClawBench 上显著优于同量级开源 baseline，并给出 pass^3、pass@3 级别结果。
- OpenForgeGUI 在 OSWorld-Verified、Online-Mind2Web、WebVoyager 上达到较高分，且在 GUI 场景与更大模型接近。
- 研究发现不同 harness 的可训练性差异明显：ZeroClaw/OpenClaw/Codex 的学习难度不同；RL 对 self-verification、工具覆盖率、多步计划成功率有正向影响。

## 适合关注的原因
- 这是“如何把 agent 从可演示推向可迭代工程系统”的关键过渡层技术。
- 对齐 benchmark 的提升并非唯一价值，更重要是降低真实部署环境中的训练样本生成成本。
- 对生产化团队而言，框架强调“可控、可复现实验”的基础设施建模思路，价值高于单模型创新。

## 局限性或待验证点
- 论文在版本中虽给出公开开源表述，但若缺少稳定代码入口，复现实践成本仍可能上升。
- 错误恢复与异常回滚能力仍被作者指出有短板，需要额外机制（如外部安全策略、重试策略）支撑。
- 部署端的策略收益很可能受限于特定 harness 实现细节，跨组织迁移代价不容忽视。

## 对后续研究/应用的启发
- 可将 OpenForgeRL 思路迁移到企业内部专有工具栈，让训练数据直接来源于真实工具闭环，而非离线脚本。
- 后续工作可把“harness 选择器”与“奖励设计器”分离，做 multi-agent 混合策略与成本约束优化。
- 推荐把该框架与 tool governance、可观测性（日志、审计）结合，构建“可追责 Agent 训练流水线”。

## 一句 Obsidian 快速浏览总结
一句话：这篇论文的核心不是新 agent 模型，而是把 harness-native 复杂执行系统变成可训练系统。

## 标准化研究框架
- **Research question：** 是否能将复杂 harness 的运行行为标准化为可学习轨迹，并通过强化学习持续提升真实部署 agent 的可靠性？
- **Literature：** 继承了 LLM agent、agentic tool-use 与强化学习微调相关研究，但补足了训练数据生成与环境接口解耦的工程缺口。
- **Theory：** 若把 harness 交互建模为马尔可夫过程中的状态-动作-反馈序列，则标准 RL 可用于持续优化策略质量与执行稳定性。
- **Hypotheses：** 在真实 harness 中训练，且统一记录反馈信号，能显著提升多步任务完成率与工具使用覆盖率。
- **Method：** 通过 proxy 收集交互轨迹，使用容器化 rollout 并在标准 RL 框架中训练，再做跨 harness benchmark 对比。
- **Data and Analysis：** 用不同 harness/环境产生日志轨迹与评测成绩，比较不同规模样本和不同 reward 设计下 pass/成功率、稳定性指标。
- **Findings：** 论文报告了多 benchmark 上显著增益，并发现 RL 对某些行为（尤其自检与长程计划）帮助明显，但 error recovery 仍待加强。
- **Conclusion：** 该方向把“可玩”agent 推向“可训、可迭代、可治理”的系统方法，属于生产化 agent 研究的重要底层能力题。
