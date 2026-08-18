# Test-Time Hallucination Control in Large Vision-Language Models

Spotlight：TTH 提供一种训练外推、可即插即用的推理时抑制机制：用 MMC 生成 token-level 验证分数，对视觉相关 token 做加权校正，兼顾效果与效率。

## 论文信息
- 论文标题：Test-Time Hallucination Control in Large Vision-Language Models
- 作者（机构）：Mehran Tamjidi, Hamidreza Dastmalchi, Ali Cheraghian, Mohammadreza Alimoradijazi, Aijun An, Hossein Rahmani（机构未在 arXiv 元信息完整展开）
- 发布日期：2026-08-11（v1）
- 主题标签：`#CV` `#LLM` `#VLM` `#Hallucination` `#Inference-time`
- 论文链接：[https://arxiv.org/abs/2608.11474v1](https://arxiv.org/abs/2608.11474v1)
- PDF 链接：[https://arxiv.org/pdf/2608.11474v1](https://arxiv.org/pdf/2608.11474v1)
- 项目/代码/数据链接（如可得）：GitHub Code：<https://github.com/Mehran-TAM/TTH>

## 论文内容
- 核心问题：LVLM 在真实场景常出现 object hallucination，现有训练型方法成本高，推理型方法或多轮、或模型特异。
- 方法概要：
  - 构建 token-validator 模块（Zero-shot Multi-Modal Classifier，MMC）
  - 对候选 token 从候选池中提取并与原始 LVLM logits 融合
  - 使用熵权重调节 token 置信度，避免内部表示被单一策略破坏
  - 全流程为 test-time 即插即用，无需训练。
- 主要贡献：
  - 提出统一框架 TTH，兼容多类 LVLM 与多个 benchmark；
  - 在保持语义覆盖的同时降低幻觉风险；
  - 给出低成本部署路径。
- 关键实验或结果：
  - 作者报告在多模型族和多 benchmark 上稳定带来准确率和鲁棒性提升（定量增益需按论文正式版本表格复核）。
- 适合关注的原因：
  - 对生产系统最关键——不改变训练流程即可显著降低幻觉，成本更低。
- 局限性或待验证点：
  - 候选 token 池与阈值依赖任务域，需要跨任务重新标定；
  - 对视觉编辑或高抽象推理任务的稳定性尚需更大规模复现实验。
- 对后续研究/应用的启发：
  - 可作为 Agent/VLM 服务链路的安全闸门模块，与检索或工具调用策略联动。
- Obsidian 快速浏览一句总结：**TTH 的核心价值是“训练外推下就把 hallucination 风险压下来”，适合直接上到现网。**

## 标准化研究框架
**Research question：** 能否在推理时仅通过 token 级校验机制降低 LVLM 幻觉，而不依赖重训练？

**Literature：** 传统 mitigation 方案常在数据/训练阶段优化参数；推理式方案多为模型特定，迁移代价高。TTH 试图给出统一即插即用替代。

**Theory：** 若可把图像条件信息映射为 token 级校验分布，并与原始解码分布进行熵敏感融合，可减少模型在不确定视觉区域输出虚构 token 的概率。

**Hypotheses：**
- H1：候选 token 约束与原始 logits 融合优于单独后处理；
- H2：熵加权比固定权重更能抑制低置信 token 幻觉；
- H3：方法对不同 LVLM 家族和任务域具有可迁移性。

**Method：** 在测试时加入 MMC token-validator，构建候选 pool；按熵进行 token-level 融合，测评多模型与多 benchmark 的生成结果。

**Data and Analysis：** 使用多个公开 LVLM benchmark 与多模型族做对照；分析幻觉率、正确率及推理开销（时间/资源）。

**Findings：** 在公开基准上 TTH 提升了鲁棒性与准确性，且未引入可观训练成本，显示部署友好性。

**Conclusion：** 对高风险视觉问答与文生图/多模态工作流，test-time 校验是一条更具工程价值的稳健路径。 
