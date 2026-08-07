> **Spotlight：** SCOPE 将“抗误导”重构为“选择性信任”：模型既要拒绝错误上下文，也不能因此学会忽略所有外部信息。MIST 的四条件配对设计，为 RAG 与 Agent 上下文可靠性提供了比单一准确率更清晰的评测方式。

# Learning When to Trust via Selective Context Preference Optimization

- **作者/机构：** Xian Sun、Wei Chow、Yingshuo Wang、Junhao Liu、Wei Gao、Qing Wu、Lingdong Kong；机构信息在 arXiv 摘要页未列出，待正文核对
- **发布日期/版本：** 2026-08-06，arXiv v1
- **主题标签：** #LLM #可信AI #上下文学习 #DPO #Benchmark #RAG
- **论文链接：** https://arxiv.org/abs/2608.06377
- **PDF：** https://arxiv.org/pdf/2608.06377
- **项目/代码/数据：** [项目页](https://worldbench.github.io/scope/)；[GitHub](https://github.com/worldbench/SCOPE)；[MIST-Bench](https://huggingface.co/datasets/worldbench/MIST-Bench)

## 核心问题

LLM 使用检索结果、工具输出或用户提示时，怎样判断上下文是否值得信任？只训练“抵抗误导”可能得到一个拒绝一切上下文的模型：表面稳健，却无法从正确证据中受益。论文因此要求模型在干净、误导、正确补充和无关四种上下文状态之间做选择性响应。

## 方法概要

作者构建人工标注的 **MIST** benchmark，把同一个推理题呈现为四种匹配条件：clean、misleading、correct-context 和 irrelevant-context。新指标 **SC2W** 统计模型在原本答对的样本上，因误导信号而从正确翻转为错误的比例。训练方法 **SCOPE** 先挖掘“clean 答对、misleading 答错”的脆弱样本，再围绕四种条件等量组织偏好对，使用标准 DPO 优化；关键点不是发明新损失，而是改变训练对的构造与平衡方式。

## 主要贡献

1. 将上下文稳健性从“越不受影响越好”改写为同时衡量拒绝错误信息和吸收有用信息的选择性信任问题。
2. 提供四条件匹配的 MIST 数据与 SC2W 配对指标，使“上下文导致的正确→错误翻转”可被直接审计。
3. 提出基于失败挖掘和均衡偏好对的 SCOPE，并在开源模型上展示降低误导脆弱性的可行性。

## 关键实验或结果

摘要报告：多种受测模型普遍存在被误导上下文翻转答案的问题；SCOPE 能显著降低流行开源模型的 SC2W，同时维持模型在 clean、correct-context 与 irrelevant-context 条件下的准确率。摘要未给出逐模型绝对数字、置信区间和训练成本，需结合正文表格再判断效果大小与稳定性。

## 适合关注的原因

这项工作直指 RAG、tool use 和长期 Agent memory 的共同风险：上下文不是越多越好，系统需要估计证据质量。其配对评测设计比混合数据上的平均准确率更容易定位因果性失败，也可迁移到网页搜索、代码代理和医疗辅助系统。

## 局限性或待验证点

- MIST 的人工构造误导是否覆盖真实检索噪声、恶意提示和多跳证据冲突，仍需验证。
- SC2W 聚焦 clean-correct 样本，不能独立衡量模型从正确上下文中“由错变对”的收益。
- DPO 后的稳健性可能依赖基座模型、偏好数据域和误导模式；跨语言与超长上下文泛化尚不清楚。
- 目前笔记依据官方摘要和项目链接，精确实验配置与数值需正文复核。

## 对后续研究/应用的启发

可把四条件设计扩展为 Agent 的工具返回值评测：同一任务分别注入正确、过期、矛盾和无关工具输出，并同时记录最终成功率与行为翻转率。应用侧还可在生成前增加显式 source reliability 预测，让模型解释“采用/拒绝哪条证据以及为什么”。

## Obsidian 快速浏览总结

**一句话：SCOPE 用配对评测和均衡 DPO，让 LLM 学习“该信时信、该拒时拒”，而不是把忽略上下文误当成稳健。**

## 标准化研究框架

**Research question：** LLM 如何抵抗误导上下文，同时保留利用正确或相关上下文的能力？

**Literature：** 对话连接上下文鲁棒性、RAG 可靠性、偏好优化和误导提示评测；现有工作常只测抗干扰，未同步测量有用上下文收益。

**Theory：** 核心概念是 selective trust：真正稳健性是对上下文质量有条件地改变预测，而非对任何上下文保持不变。

**Hypotheses：** 非社会科学假设检验；等价技术假设是，利用匹配失败样本并均衡四类偏好对，可降低错误翻转而不损害其他条件准确率。

**Method：** 构建 MIST 四条件 benchmark 和 SC2W 指标；挖掘脆弱样本，以 DPO 训练 SCOPE。

**Data and Analysis：** 人工标注的匹配推理题；比较多种开源模型在四条件下的准确率与 clean-correct→misleading-wrong 配对翻转。

**Findings：** 误导脆弱性在受测模型中普遍存在；SCOPE 据摘要可显著降低 SC2W，并保持其他上下文条件表现。

**Conclusion：** 上下文可靠性评测应奖励选择性信任，而不能把全面忽略上下文当作鲁棒性成功。

