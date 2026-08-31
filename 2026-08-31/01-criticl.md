# CritICL: Inference-Time Weak-to-Strong Generalization from Small Language Model Failure Modes

> Spotlight（2 句）：论文把“LLM 推理失败模式”转成可显式利用的推理线索，在 inference-time 阶段以更低成本提升推理质量。它不是盲目扩样本，而是将弱模型可见的错误结构改写成可迁移的控制信号，适合在服务端推理链路里直接落地验证。

## 基本信息
- 论文标题：CritICL: Inference-Time Weak-to-Strong Generalization from Small Language Model Failure Modes
- 作者：Yufan Wu, Yinghui He, Zhengyi Hu, Lang Wei, Ruichen Li, Qifan Yang, Ting Zhu（机构未在 arXiv 页面完整披露）
- 发布日期（版本）：2026-08-27（v1）
- 主题标签：`#LLM` `#Reasoning` `#Inference-Time` `#ICL` `#Failure-Aware` `#Efficiency`
- 论文链接：[https://arxiv.org/abs/2608.27455](https://arxiv.org/abs/2608.27455)
- PDF 链接：[https://arxiv.org/pdf/2608.27455v1.pdf](https://arxiv.org/pdf/2608.27455v1.pdf)
- 项目/代码/数据链接：
  - Code: [https://github.com/umwyf/CRITICL](https://github.com/umwyf/CRITICL)
  - 数据：未公开

## 核心问题
在推理阶段，传统 test-time scaling 往往依赖重复采样或外部 verifier，推理成本高且难以控制。作者尝试把“失败”本身变成资源：弱模型的失败模式能否在不显著增量成本的情况下，稳定提速并提升大模型推理质量？

## 方法概要
1. 从同一模型家族内不同规模模型抽取“失败模式”并建模其结构可迁移性。  
2. 推理时从历史失败模式检索失败证据，组装为可插入 prompt 的 critique example。  
3. 设计两套策略：
   - CritICL-dynamic：按输入自适应预测失败类型并检索对应纠偏样例；
   - CritICL-static：使用全局失败画像提供稳定指导。  

## 主要贡献
- 提出在 inference-time 引入失败模式结构的机制化方法，突出“错误可学习性”。
- 在保持高采样/低 token 的前提下，给出更接近 test-time scaling 效果的替代线。
- 首次将模型族内失败行为系统化为 lightweight 的推理增强接口，兼顾效果与部署友好性。

## 关键实验或结果
- 在不同推理场景下，CritICL 系列在性能上稳定领先于标准 ICL，部分情形可达到或超越更重型 test-time scaling 方法。
- 相比多次重采样策略，生成次数与 token 成本显著下降。
- 公开实验显示“小模型失败模式”并非纯噪音，而是可复用的提示先验。

## 适合关注的原因
- 论文目标直接贴近实际在线推理的成本瓶颈，不是纯理论改进。
- 方法对推理链路侵入小，易与现有服务集成。
- 对后续“轻量推理优化”方向提供了与“更大推理预算”并行的替代思路。

## 局限性或待验证点
- 失败模式提取与泛化边界未充分覆盖跨领域长尾任务。
- 对高噪声数据下失败模式漂移的鲁棒性仍需实测。
- 成本收益曲线（延迟、吞吐、稳定性）需要更多公开 ablation。

## 后续研究/应用启发
- 可直接嵌入 Agent planner 或 RAG 复核链路，做“动态 critique-prompt generator”。
- 可扩展为模型版本间知识迁移机制：不同规模模型共享失败语料库。
- 与 verifier/critic 级联时，形成失败闭环数据库，支持在线自举更新。

## 适合 Obsidian 快速浏览的中文总结
一句话：先把小模型失败模式变成“可复用的推理教学样例”，再用最少 token 数完成更稳健的 LLM 推理增强。

## 标准化研究框架
- **Research question：** 在给定同类 LLM 家族时，小模型失败模式是否可在 inference-time 被系统化重用，从而显著提升 reasoning 性能并降低推理成本？  
- **Literature：** 相比传统 test-time scaling、self-consistency 与多采样 verifier 流水线，本文尝试用失败结构作为新型 prompting 信号。  
- **Theory：** 假设失败模式在模型家族内具有可迁移结构，且可作为条件化控制变量参与 ICL。  
- **Hypotheses：** ①动态检索更灵活；②failure-aware ICL 可在多数任务上优于标准 ICL；③token/延迟可明显下降。  
- **Method：** 两套模型（dynamic/static）在推理阶段插入失败模式控制信息，并与 baseline 做多任务对照。  
- **Data and Analysis：** 对比标准 ICL、传统 test-time scaling，重点分析性能-代价二维指标。  
- **Findings：** 性能与效率同步提升，支持“失败模式可复用”这一机制假设。  
- **Conclusion：** 在真实服务里，这是一个低门槛、低成本的推理增益方向，但跨域稳健性仍需更长尾验证。

