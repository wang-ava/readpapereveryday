# ExtractBench: A Benchmark for Schema-Guided Enterprise Document Extraction

Spotlight：该工作首次把“schema-guided extraction”与可追溯性、准确率、成本三类指标放在同一评测体系，推动企业文档 agent 从只追求抽取准确性转向“可落地可审计”的全栈评测。

- 论文标题：ExtractBench: A Benchmark for Schema-Guided Enterprise Document Extraction
- 作者：Boyang Zhang；Adrian Lyjak；Eli Stewart；Zhaoqi Li；Simon Suo
- 机构（如可得）：arXiv 条目未直接给出机构信息
- 发布时间：2026-07-31（v1）
- 主题标签：`#Agent` `#Enterprise` `#RAG` `#Document` `#Evaluation`
- 论文链接：[https://arxiv.org/abs/2607.29677v1](https://arxiv.org/abs/2607.29677v1)
- PDF 链接：[https://arxiv.org/pdf/2607.29677v1](https://arxiv.org/pdf/2607.29677v1)
- 项目/代码/数据链接：
  - 数据集：[https://huggingface.co/datasets/llamaindex/ExtractBench](https://huggingface.co/datasets/llamaindex/ExtractBench)
  - 代码：[https://github.com/run-llama/ExtractBench](https://github.com/run-llama/ExtractBench)

## 核心问题
企业文档提取场景通常有长表格、长列表和跨页归属关系，agent 的输出往往缺乏可追溯 evidence，而且不同方法在“准确率”和“成本”之间没有统一对标。

## 方法概要
作者搭建 schema-guided extraction 任务池，定义四个核心评测轴：
- value accuracy
- record completeness
- grounding（word-level/page-level 可追溯性）
- cost（计算与 token 成本）

通过混合标注流程（真实文档一致性共识、合成列表真值、人工复核表单）构造规模较大的企业文档集。

## 主要贡献
- 建立包含 4,869 页的规模基准，覆盖 370 份文档、8 个业务域、67 种文档类型。
- 将 extraction 的“结果正确性+完整性+可追溯性+花费”联合指标化。
- 提供公开数据与评测基线，比较 VLM、Coding Agent 与不同抽取策略。

## 关键实验或结果
- 报道该数据集中含明确难度标签，可定位不同文档挑战类型。
- 在指标综合上，LlamaExtract Agentic Plus 在 value accuracy / record completeness / grounding 方面综合领先。
- VLM 在短文档上具备较高准确率，但在长列表时易截断记录；Coding Agent 成本更高但完整性更好。

## 适合关注的原因
这是企业级 AI 产品直接能用的 benchmark 结构：从“能不能抽对”升级为“抽对得有证据、也不能太贵”，适合选型和治理。

## 局限性或待验证点
- 论文以英文企业文档为主，跨语言与多语法档案环境下表现未知。
- 真实企业部署还需补充隐私与权限分区压力测试。
- 成本定义未统一到统一货币单位，需要结合服务提供方重标定。

## 对后续研究/应用的启发
- 可用于评估文档 agent 的上线前风控门槛（例如需达到最低 grounding/F1 线）。
- 可将 schema 模板策略与自动化回放测试结合，提高回归测试效率。
- 适合转为“合规抽取”基线：不仅看值，还要看证据链完整度。

## Obsidian 快速浏览总结
一句话：ExtractBench 把企业文档提取的 benchmark 目标从单指标抽取准确率扩展到可审计的三维质量体系，适合构建真实生产闭环。

## 标准化研究框架
- **Research question：** 企业文档提取任务中，如何同时评估正确性、完整性、可追溯性和成本？
- **Literature：** 对齐前沿 extraction benchmark，但补齐了 grounding 与成本两个长期缺失指标。
- **Theory：** 文档抽取的“可用性”是多目标权衡问题；只优化单一 accuracy 会放大漏抽和幻觉风险。
- **Hypotheses：** 在统一框架下，agent 与 code-based 方法会在长文档与表单场景出现显著差异，且成本差异足以影响方案选择。
- **Method：** 构建 4,869 页多域数据集，并定义 value / completeness / grounding / cost 指标进行统一评测。
- **Data and Analysis：** 结合真实文档一致性与合成标签做对照实验，报告多模型对比和策略敏感性分析。
- **Findings：** 抽取任务中可追溯性与成本会显著重排模型排名，短文档优劣不代表长文档可用性。
- **Conclusion：** 该基准为企业 AI 工作流提供了可落地的评估坐标系，可直接用于模型治理与版本验收。
