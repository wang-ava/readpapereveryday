---
spotlight: "CritICL 用小模型失败模式做"推理引导"的单趟推理提升，既提升 LLM 逻辑表现又降低推理成本，值得关注其对轻量化推理的范式价值。"
---

# CritICL: Inference-Time Weak-to-Strong Generalization from Small Language Model Failure Modes

## 基本信息
- **论文标题**：CritICL: Inference-Time Weak-to-Strong Generalization from Small Language Model Failure Modes
- **作者**：Yufan Wu, Yinghui He, Zhengyi Hu, Lang Wei, Ruichen Li, Qifan Yang, Ting Zhu
- **机构**：arXiv 页面未公开机构，建议在论文全文或项目主页补充
- **发布日期 / 版本日期**：2026-08-27（v1）
- **主题标签**：`LLM` `Inference-time` `In-Context Learning` `Failure Analysis`
- **论文链接**：https://arxiv.org/abs/2608.27455
- **PDF 链接**：https://arxiv.org/pdf/2608.27455
- **项目/代码/数据链接**：[Code](https://github.com/umwyf/CRITICL)

## 核心问题
当前推理时放大（test-time scaling）通常依赖重复生成或额外验证步骤，成本高且易失控。如何利用模型在弱模型尺度上可观察的失败模式，让强模型在推理时高效修正错误？

## 方法概要
- 提出 CritICL 框架，在推理时显式引入“失败模态”提示。
- 关键假设：同一模型家族中，小模型的失败模式在结构上对大模型可迁移，可作为有效的 in-context critique。
- 设计两种变体：
  - **CritICL-dynamic**：按输入预测并检索最相关的 failure modes；
  - **CritICL-static**：预先构建全局失败模态画像，作为稳定的推理指导。
- 在推理上下文中加入 critique 示例，替代纯粹的“盲目再采样”。

## 主要贡献
1. 将“失败”从负例转为可复用的推理信号，给出 failure-driven inference 的明确范式。
2. 提出可复现的动态/静态双分支方法，兼顾适应性与稳定性。
3. 在推理效率上明确对比了传统 token 代价更高的放大策略。

## 关键实验或结果
- 实验表明 CritICL 在多个基准上持续优于标准 in-context learning。
- 与 test-time scaling 方法相比，多数场景达到可比甚至更优效果，同时降低生成次数与 token 成本。
- 论文强调其收益并非靠更多采样，而是靠更有结构的信息注入。

## 适合关注的原因
- 对企业内部模型服务（高并发、成本敏感）有直接启发：在不显著加重推理预算前提下提升推理鲁棒性。
- 与传统 self-consistency、verifier pipeline 相比，框架更轻量，易与现有 API 流程对接。

## 局限性或待验证点
- 论文主要通过现有失败模式抽取与重组实现提升，是否跨领域、跨任务规模稳定，需要更多公开复现实验。
- 失败模式质量依赖于“弱模型覆盖面”；若弱模型本身偏差明显，可能把有害模式放大。
- 代码可复现性需关注数据过滤与检索细节，建议持续检查公开脚本与超参。

## 对后续研究/应用的启发
- 可将 CritICL 思路扩展到检索增强、tool-use、agent chain 思路，让“失败回放”成为统一的在线修正信号。
- 适合与 uncertainty-aware decoding 联合，构建“失败模态置信度触发器”，按任务难度自动切换动态/静态策略。

## 一句话中文速览总结
CritICL 用小模型失败案例作为推理线索，在推理阶段显著减少盲目再生成，兼顾效果提升与成本控制。

## 标准化研究框架
- **Research question：** LLM 是否能在推理时利用弱模型失败模式，实现更强的泛化与更低代价的错误校正？
- **Theory：** 依托 In-Context Learning 与模型尺度内结构可迁移假设：失败模式包含可泛化的任务语义约束。
- **Hypotheses：** 将故障提示（failure critique）显式注入上下文，可提升推理准确率并显著减少重采样开销。
- **Method：** 从弱模型输出中提取故障模式，构建动态/静态 critique 集合；在推理阶段作为结构化上下文引导预测。
- **Data and Analysis：** arXiv 提供的实验设置中对比标准 ICL 与常见 test-time scaling 方法；分析 token 成本、成功率/得分等指标。
- **Findings：** 论文声称 CritICL 在关键任务上持续优于基线且 token/计算开销更低。
- **Conclusion：** Failure-as-guide 是值得推进的轻量推理增强路径，但仍需跨域稳健性和偏差传播的深入评估。
