# Sibyl: Temporal Backtesting for Literature-Based Scientific Discovery with Large Language Model Agents

Sibyl 用多智能体 LLM 管道做“时间切片”式科学文献挖掘，把“可检验性”的科学预测作为主目标，并用回测框架评估假说的确认率。

- **论文标题**：Sibyl: Temporal Backtesting for Literature-Based Scientific Discovery with Large Language Model Agents
- **作者/机构**：Blagoy Rangelov（Texas State University）
- **发布日期/版本日期**：2026-06-06（Published: 30 May 2026, Last Modified: 06 Jun 2026, ICML2026-AI4Science）
- **主题标签**：#AI4Science #AgenticAI #ScientificDiscovery #TemporalBacktesting #KnowledgeBase
- **论文链接**：<https://openreview.net/forum?id=xfLV86qoBd>
- **PDF 链接**：<https://openreview.net/attachment?id=xfLV86qoBd&name=pdf>
- **项目/代码/数据链接（如可得）**：当前条目未提供公开仓库链接；文中提到将补充完整实验产物。
- **核心问题**：传统 LLM 科学推断常缺少可复验性与时间一致性，论文聚焦如何避免“看过答案再推测”导致的虚假预测能力。
- **方法概要**：
  1. 设定时间切分点：使用训练语料仅在 cutoff 前，并在 cutoff 后语料中验证预测。
  2. 将文献提取为可结构化 claim（关联/反关联/未发现/预测/开放问题）并记录来源文本。
  3. multi-agent 协作生成“可实验化、可证伪”的科学假说。
  4. 用后验语料进行 temporal backtesting，估计预言命中率与污染风险。
- **主要贡献**：
  1. 引入了“时间切片回测”用于 agentic 科学发现评估；
  2. 在同一流水线内完成 claim 结构化、预测生成和回测验证；
  3. 提出 provenance 审计协议，显式追踪 citation hallucination 与污染路径。
- **关键实验或结果**：在 X-ray binary 天体物理作为验证域中，系统处理 14,400 篇经过筛选论文、抽取 11,000+ 结构化 claim，生成 60 条预测，18%（11 条）在后验文献中被确认，保守过滤下确认率仍保持 12.5%–18%。
- **适合关注的原因**：
  1. 给 AI 科学发现提供了更接近科学实验范式的验证闭环；
  2. 通过时间约束抑制了“先验泄露”；
  3. 其结构化 claims 形式适合与知识图谱、文献数据库系统集成。
- **局限性或待验证点**：
  1. 数据与模型依赖于文献抓取质量与元信息标准化程度；
  2. 目前偏重天体物理示例，泛化到生物/材料/社会科学待测试；
  3. 当前还需更完整的公开复现实验包。
- **对后续研究/应用的启发**：可用于科学情报、文献挖掘平台，尤其适合“可证伪预测优先”的研究流程设计。
- **Obsidian 快速浏览一句总结**：Sibyl 用时间回测把科学假说从“文学畅想”变成可量化、可复验的检验任务。

## 标准化研究框架
- **Research question：** 在保证时间一致性的前提下，LLM agent 能否持续产出可证伪科学预测并在后验文献中体现验证价值？
- **Literature：** 对齐 AI-for-Science、文献知识抽取与模型生成式假说评估方向，核心在于将“可检验性”显式嵌入生成流程。
- **Theory：** 等价于建立一个带时间边界的监督循环：训练信息必须来自 cutoff 前，验证任务在 cutoff 后执行。
- **Hypotheses：** 以结构化 claim 和 provenance 审计约束的 pipeline 能降低 hallucination 与污染，提高预测可信度。
- **Method：** 构建多智能体流水线、时间切片回测、敏感性过滤（逐级保守化）并统计确认率。
- **Data and Analysis：** 使用 X-ray binary 语料中的 pre/post cutoff 文献进行回测，重点分析确认率、污染类型（泄露/时序泄漏/幻觉引用）和失败模式。
- **Findings：** 在当前域内实现了可重复的可验证预测产出；部分假说能够在未见语料后得到后验支持。
- **Conclusion：** 为 AI4S 提供了可落地的“预测—回测—审计”闭环方法，后续可扩展到更多学科。
