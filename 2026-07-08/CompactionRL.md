# CompactionRL: Reinforcement Learning with Context Compaction for Long-Horizon Agents

长程 agent 的上下文窗口会很快触顶，这篇把“上下文压缩”从推理阶段技巧升级为训练目标的一部分。论文尝试让模型在被压缩后的上下文中继续决策并学习压缩策略，从而提升长期任务稳定性。

- 论文标题：CompactionRL: Reinforcement Learning with Context Compaction for Long-Horizon Agents
- 作者：Yujiang Li, Zhenyu Hou, Yi Jing, Jie Tang, Yuxiao Dong
- 机构：arXiv 元信息未提供完整机构字段（建议核验作者主页）
- 发布日期：2026-07-06（v1）
- 主题标签：#Agent #ContextCompaction #Reinforcement Learning #Long-horizon
- 论文链接：https://arxiv.org/abs/2607.05378v1
- PDF 链接：https://arxiv.org/pdf/2607.05378v1
- 项目/代码/数据：未在 arXiv 元信息中给出公开链接

## 核心问题

长时间交互时 agent 的轨迹超出窗口，压缩摘要常常丢失关键约束或推理线索，影响后续动作质量。如何把“压缩质量”直接纳入学习目标？

## 方法概要

论文提出在 RL 训练中联合优化两个部分：
- 任务执行（primary task reward）
- summary 生成质量（summary objective）

采用 token-level loss normalization 与跨轨迹 generalized advantage estimation，训练模型在 compacted trajectory 上学习，减少上下文长度不一致导致的不稳定。

## 主要贡献

1. 提出 CompactionRL 训练范式：让模型同步学习“做事”和“如何压缩”两件事。
2. 在开源大模型上验证后，显示对长程代码 agent 有显著提升。
3. 在部署链路（RL pipeline）中可直接接入 GLM-5.2 等大模型训练流程。

## 关键实验或结果

- GLM-4.5-Air（106B-A30B）在 SWE-bench Verified 的 Pass@1 达到 66.8%。
- 同组模型在 Terminal-Bench 2.0 达到 24.5%，均有绝对增益（7.0 与 3.1 点）。
- GLM-4.7-Flash（30B）也有 5.5 与 6.8 点提升，说明方法对不同规模有效。

## 适合关注的原因

agentic coding、自动化运维、逐步工具调用类系统最受上下文衰减影响，该方法直接命中“可部署的长程稳定性”痛点，且与现有 RL 后训练链路兼容度高。

## 局限性或待验证点

1. 未见所有任务类型的公开泛化曲线，跨域鲁棒性仍需更多验证。
2. 压缩策略加入是否会系统性偏向短期奖励，未来应评估长期一致性。
3. 公开代码未见可直接复现入口，当前可复现实践需等待补充。

## 对后续研究/应用的启发

可将其用于统一“记忆模块 + 压缩模块”的架构设计，尤其在高频工具调用场景把摘要质量作为可控策略超参，而不是硬规则窗口切分。

一句中文总结：这篇把上下文压缩从“事后删减”改成“训练可学能力”，对长程 agent 非常有操作性。

## 标准化研究框架

- **Research question：** 是否能通过 RL 显式训练 context compaction，降低长程代理在上下文截断下性能退化？
- **Literature：** 继承长程 agent 中记忆压缩与策略蒸馏方向，但把压缩与策略学习绑定，减少独立后处理。
- **Theory：** 假设合适的 reward decomposition 与 compacted-state训练可提升策略对关键历史信息的保持能力。
- **Hypotheses：** 与仅后处理压缩相比，联合学习会在长期任务中提升 Pass@1 与鲁棒性。
- **Method：** 在训练时同步学习任务动作与 summary 的策略，使用 token-level 归一化与跨轨迹 GAE 更新。
- **Data and Analysis：** 采用 open models + 长程 agent coding 类 benchmark，比较 baseline 与 CompactionRL 在 SWE-bench Verified / Terminal-Bench 2.0 的差异。
- **Findings：** 文内报告稳定正向增益，且对不同规模模型都成立。
- **Conclusion：** 本工作支持“上下文压缩可被学习”的结论；该方法不属于传统社会科学假设检验，等价于在优化目标上加入可学习记忆保真机制。
