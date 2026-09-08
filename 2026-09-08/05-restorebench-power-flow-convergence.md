---
spotlight: "首个面向电网潮流不收敛场景的 agent 基准，覆盖 2 个电网、46 例任务，为 LLM 在工程决策中的可执行性评估提供了可复现标准。"
---

# RestoreBench: Can AI Agents Restore Power Flow Convergence?

## 基本信息
- **论文标题**：RestoreBench: Can AI Agents Restore Power Flow Convergence?
- **作者**：Riccardo Mansutti, Andrea Pomarico, Robert Jakob, Qian Zhang, Alberto Berizzi, Kevin O'Sullivan
- **机构**：未在 arXiv 元数据首屏给出
- **发布日期 / 版本日期**：2026-08-31（v1）
- **主题标签**：`AI4S` `电力系统` `agentic AI` `基准构建` `工具调用`
- **论文链接**：https://arxiv.org/abs/2609.00384v1
- **PDF 链接**：https://arxiv.org/pdf/2609.00384v1
- **项目/代码/数据链接**：https://github.com/Mansutti081/RestoreBench（代码与基准）

## 核心问题
潮流不收敛在电力系统运行中是常见故障，但现有评测多关注单次预测模型，很少覆盖 LLM agent 的多步诊断与执行能力。如何评估 agent 在真实工程动作链路中的可用性？

## 方法概要
- 构建 RestoreBench 基准，明确 observation space、action space 与评价指标。
- 设计模拟环境并提供可复现实验接口，评测 chatbot、single-agent、multi-agent 三种架构。
- 每个案例要求 agent 在 constrained action space 中执行一条或多条调整动作恢复收敛。
- 通过统一的任务接口把推理、工具调用和状态反馈串成闭环。

## 主要贡献
1. 给 AI4S（电力系统）提供了首个围绕“恢复潮流收敛”设计的 agent 评测环境。
2. 明确三类 agent 架构在统一任务定义下的比较维度：成功率、动作步数、稳定性与可解释性。
3. 推动 LLM 在工程决策中的安全部署讨论，从“是否会回复”转向“能否在受限动作里正确闭环执行”。

## 关键实验或结果
- 涵盖 2 个电网、每网 46 个不收敛案例（共 92 个任务实例）。
- 每个实例需要至少一条 corrective action，形成多步决策链测试。
- 基准显式记录动作可行性与收敛恢复效果，形成可追踪排名与可复现实验路径。

## 适合关注的原因
AI in Science 的关键瓶颈不是单次预测准确率，而是多步工程闭环安全。RestoreBench 直接把评测重心放到“执行能力+动作约束+可复现性”，与真实电网应用更贴近。

## 局限性或待验证点
- 当前覆盖仅 2 个电网与 46 个场景，不代表所有实时网络工况。
- 评测基于模拟环境，真实现场部署还涉及通信、延迟与人工审批因素。
- 论文对不同架构之间的性能差异未在摘要给出具体数值，需读全文确认。

## 对后续研究/应用的启发
- 可扩展为跨地区电网、跨事故等级的统一评测库，形成“agentic 运维排行榜”。
- 同类框架可迁移到储能、天然气网络、微网控制等关键基础设施运维任务。
- 未来可加入安全合规模块，在 action 执行阶段加入人机双签或阈值审批。

## 一句话中文速览总结
这是一个把 AI4S 与 agent safety 结合起来的基准，关注的是“LLM 能否在约束环境里稳定恢复系统状态”。

## 标准化研究框架
- **Research question：** 在电力系统潮流不收敛场景下，LLM agent 的多步决策是否能稳定恢复系统收敛？如何公平比较不同架构？
- **Literature：** 与传统潮流算法或单模型预测不同，本文从决策闭环视角切入，以基准而非单模型评分作为核心对象。
- **Theory：** 将恢复问题视为在约束动作空间中的序贯决策过程，评估目标是从“不收敛”状态转移到“收敛”状态。
- **Hypotheses：**（1）多步智能体在相同环境下优于单步回复模型（2）不同架构可通过统一指标比较稳定性和风险—收益权衡（3）统一任务定义有助于可复现公平对比）。
- **Method：** 构建 RestoreBench 的任务包、动作编码器和评分器，分别运行 chatbot / single / multi-agent 三类方法并收敛判定。
- **Data and Analysis：** 使用 2 个电网的 92 个 case，记录恢复成功率、动作路径、收敛步数和约束合规指标。
- **Findings：** 基准建立了可复现实验链路，并为 3 类架构提供对照框架；多步交互能力成为区分模型的关键轴。
- **Conclusion：** 在 AI4S 工程场景中，动作空间约束下的多步决策评估比静态指标更具部署相关性，RestoreBench 提供了可扩展起点。
