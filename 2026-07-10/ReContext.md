# ReContext: Recursive Evidence Replay as LLM Harness for Long-Context Reasoning

ReContext 非常直接地回应了 LLM 在长上下文里“看得见但没用上”证据的问题，用训练外的推理阶段重排证据策略，让模型在不改参数的情况下显著提升长上下文推理效率。

## 论文基本信息
- 论文标题：ReContext: Recursive Evidence Replay as LLM Harness for Long-Context Reasoning
- 作者/机构：Yanjun Zhao 等（arXiv 页面未提供机构信息）
- 发布日期/版本日期：2026-07-02（v1）
- 主题标签：#LLM #长上下文 #推理 #检索增强 #无监督推理增强
- 论文链接：[https://arxiv.org/abs/2607.02509](https://arxiv.org/abs/2607.02509)
- PDF 链接：[https://arxiv.org/pdf/2607.02509](https://arxiv.org/pdf/2607.02509)
- 项目/代码/数据链接：代码仓库 [https://github.com/Yanjun-Zhao/ReContext](https://github.com/Yanjun-Zhao/ReContext)

## 核心内容解读
- 核心问题：现有 LLM 虽支持更长上下文，却常未能有效利用输入中的关键证据，导致长问题回答仍然掉线。
- 方法概要：提出 Recursive Evidence Replay（递归证据回放）作为推理后处理步骤。方法先基于模型内部相关性信号构建 query 条件化证据池，再在最终生成前反复回放这些证据，不剪裁原始上下文，也不引入外部检索。
- 主要贡献：
  1) 提出一套训练免费且可直接叠加到现有 LLM 的长上下文增强流程；
  2) 将上下文处理解释为“记忆-检索-回放”的框架并给出理论分析；
  3) 在多个长上下文数据集上系统验证该策略的泛化提升。
- 关键实验或结果：在 8 个长上下文数据集上、128K 上下文长度条件下，Qwen3-4B / Qwen3-8B / Llama3-8B 上均显示持续增益，并报告在三类模型上均获得最佳平均排序表现。
- 适合关注的原因：对“inference-time optimization」路径很实用，尤其适合资源有限情况下提升企业内测 LLM 服务的长上下文命中率，不必立即再训练。
- 局限性/待验证点：
  1) 证据池构建依赖模型内部相关性信号，不同模型可能稳定性差异大；
  2) 长上下文任务类型外推性（如代码修复、数学证明）仍需更多跨任务验证；
  3) 仍有额外推理代价，需要在 latency 与精度间做工程级平衡。
- 对后续研究/应用启发：可尝试与工具调用、检索增强（RAG）和多轮对话记忆机制拼接，形成统一的“上下文质量控制层”，而不是只追求窗口长度扩展。

一句话速览：RECONTEXT 用“先选证据、再重放”替代“盲目吃满上下文”，用更轻量的推理流程显著改善 LLM 的实用长上下文表现。

## 标准化研究框架
**Research question：** 在不改模型参数的前提下，如何让 LLM 在超长上下文中更有效地利用输入证据而非只“看到”信息？
**Literature：** 以往方法多依赖上下文窗口扩展、RAG 或蒸馏式训练增强，本工作与这些方向相比更偏向推理时证据选择与重放机制。
**Theory：** 将上下文看作 memory store，query 为检索 cue，注意力为 cue-trace 关联，并用复现重放（replay）机制来激活关键痕迹。
**Hypotheses：** 如果在输出前加入证据重放，那么在不缩减上下文的情况下可提高证据利用率；且在不同模型架构间具有一定跨模型稳健性。
**Method：** 基于内部相关性信号构造 query 条件化证据池；递归选择并回放高价值证据；保留原始上下文；无训练部署。
**Data and Analysis：** 在 8 个长上下文基准数据集、128K context length 下评估多模型对照实验，并比较不同模型规模（Qwen3-4B/8B, Llama3-8B）。
**Findings：** 多模型和多任务均观察到统一收益，并给出平均排名优势；说明方法具备一定泛化性。
**Conclusion：** RECONTEXT 为长上下文推理提供了实用的“推理时增强层”，不是模型替换，而是可复用的推理协议。
