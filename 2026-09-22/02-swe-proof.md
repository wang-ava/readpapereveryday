Spotlight：通过测试仍可能留下错误，而形式化验证的瓶颈常在“规格是否忠实表达需求”。SWE-Proof 将真实仓库问题转成可检验的形式化任务，同时明确证明所依赖的信任边界。

# SWE-Proof: Can Language Models Resolve Real-World Issues with Machine-Checked Proofs?

## 论文信息

- 作者：George Ma、Benjamin Mikek、Haoyu Li、Ferhat Erata、Yuhao Zhang、Zeren Shui、Behrooz Omidvar Tehrani、Jun Huan、Murali Krishna Ramanathan、Somayeh Sojoudi、Hao Zhou、Anoop Deoras。
- 机构：UC Berkeley、Georgia Tech、UIUC、AWS AI Labs。
- 发布日期：2026-09-18（UTC）；阅读版本：arXiv v1。
- 主题标签：#AI论文 #LLM #代码Agent #形式化验证 #评测
- [论文](https://arxiv.org/abs/2609.21190v1) · [PDF](https://arxiv.org/pdf/2609.21190v1) · [正文](https://arxiv.org/html/2609.21190v1)。
- 项目/代码/数据：论文描述发布工件及其结构，本次未找到并核实独立下载入口；不能据此断言已经可以完整复现。
- 阅读范围：摘要、Benchproofer、实验表 2、局限与相关附录；未执行验证器。

## 核心问题

真实 issue 的自然语言需求如何变成可信规格？即使实现通过证明，能否保证它对应实际补丁并满足原始意图？

## 方法概要

Benchproofer 利用已知正确补丁构建规格、参考实现和未修改函数的环境公理，再以机械检查、变异检查、模糊测试和对抗审查把关。评测区分模型自己写规格与直接获得正确规格，并使用 Nagini、Velvet、Lean 等后端。[方法](https://arxiv.org/html/2609.21190v1#S3)

## 主要贡献

形成覆盖 SWE-bench Verified 500 个问题的 SWE-Proof；将“通过测试”“满足形式规格”“规格忠实性”拆成不同评估对象。[摘要及版本页](https://arxiv.org/abs/2609.21190v1)

## 关键实验或结果

正文表 2 的 Opus 4.8 结果：基线测试通过率 85.0%；额外对抗审查后为 58.2%；提供规格并要求验证的 Nagini 设置为 95.0%。这三项通过条件不同，不能作为完全同口径的增益直接相减。只提供定位信息时为 88.2%，也说明规格收益需考虑定位帮助。模型自行构造规格的设置没有稳定超越基线；摘要报告其规格约 62% 通过审查。[实验与指标定义](https://arxiv.org/html/2609.21190v1#S4)

## 适合关注的原因

适合代码 Agent 评测与可靠软件生成研究：验证器只能回答形式对象的问题，如何表达真实需求仍需独立评价。

## 局限性或待验证点

作者明确说明“验证意味着解决问题”并非端到端定理：自然意图到规格、环境公理到真实函数、形式实现到 Python 补丁存在审查边界。LLM 审查票决是经验证据，不是证明；少数实例需人工建模或放宽信息披露限制。[局限](https://arxiv.org/html/2609.21190v1#S5)

我的判断：下一步应以独立人工规格审计和新仓库复验，检查同类模型共享盲点；原测试未发现反例，也不能等同补丁无错误。

## 对后续研究/应用的启发

建议分别训练规格生成、反例搜索和代码修复模块，并保留自然需求到每条约束的可追溯映射。评测时同时公布测试、证明、规格审计三种结果，避免单个“成功率”掩盖差异。

## 中文一句速览

证明的可靠性，取决于被证明的规格与实际需求是否一致。

## 标准化研究框架

**Research question：** 如何为真实仓库修复建立比测试更强的正确性评估？

**Literature：** 连接 SWE-bench、形式化代码生成与自然语言规格合成。

**Theory：** 等价于带前提的程序正确性框架；证明对形式模型有效，外部对应关系需审计。

**Hypotheses：** 属于工程对照命题：正确规格可能有益，自写规格是否同样有效需实测。

**Method：** 构建验证任务，对照规格、定位及验证工具的不同供给设置。

**Data and Analysis：** 500 个问题；按各设置的通过条件统计，检查规格与反例。

**Findings：** 正确规格有帮助，自动规格忠实性仍是瓶颈；不能混淆不同评分口径。

**Conclusion：** 形式验证值得引入，但规格质量和代码对应关系必须单独报告。
