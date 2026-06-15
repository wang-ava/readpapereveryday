# Late-Layer Fusion is Enough: Dual-Path Vision Token Routing for Multimodal Large Language Models under Visual Saturation

这篇论文的主张很清晰：LLM 的深层层次并不适合对视觉 token 与语言 token 一刀切处理。作者通过实证观察“视觉 token 饱和”现象，给出可训练、低开销的双路径路由策略。

- **论文标题**：Late-Layer Fusion is Enough: Dual-Path Vision Token Routing for Multimodal Large Language Models under Visual Saturation
- **作者/机构**：Siyuan Liu, Jinyang Wu（arXiv 页面未统一披露完整机构）
- **发布日期/版本日期**：2026-06-08（`v1`）
- **主题标签**：#LLM #MLLM #EfficientInference #VisionToken #ModelDesign #CrossModal
- **论文链接**：<https://arxiv.org/abs/2606.09131>
- **PDF 链接**：<https://arxiv.org/pdf/2606.09131v1>
- **项目/代码/数据链接（如可得）**：目前未在 arXiv/Hugging Face 页面直接见到公开代码链接；可继续追踪后续 release。
- **核心问题**：多模态模型通常让图像 token 与文本 token 在同样深度路径中共同计算，造成冗余计算和视觉表示漂移，尤其在任务适配阶段不稳定。
- **方法概要**：
  1. 先做层级分析：发现视觉 token 在 LLaVA-1.5 中约在中层即达到饱和。
  2. 提出 DPVR（Dual-Path Vision Token Routing）。
  3. 核心实例 DPVR-LF：在饱和点将视觉 token 路由到一层可训练侧支，主路径仅保留文本 token 的深层处理。
  4. 在最终层做视觉-文本重融合，减少深层重复视觉计算。
- **主要贡献**：
  1. 提出“模态异步路由”思路，挑战经典对称 Transformer 处理的默认假设。
  2. 用仅约 3% 可训练参数实现性能-效率折中。
  3. 明确指出 late fusion 在一定条件下足以保持强表征能力。
- **关键实验或结果**：
  - 在标准 MLLM 基准上保持竞争性能的同时，减少了深层视觉 token 的计算负担。
  - 实验证明文本与视觉 token 的异步处理对效率与稳定性更友好。
- **适合关注的原因**：
  1. 成本与精度平衡是 MLLM 落地关键，文章给出工程上可直接尝试的结构改造。
  2. 模型可训练参数仅小幅增加，适配现有 LMM 时改造成本低。
  3. 对多模态推理的“哪里保留视觉、哪里稀释视觉”提供了可复制范式。
- **局限性或待验证点**：
  1. 目前样本主要基于公开 LLM 家族与任务；不同架构下迁移需验证。
  2. 论文对超参数敏感性未给出全面扫描。
  3. 对复杂长序列、动态视觉场景的长尾表现尚待补充。
- **对后续研究/应用的启发**：可用于 MLLM 推理服务端的推理加速模块，并作为后续“层级模态路由 + 动态稀疏”研究的基线。
- **Obsidian 快速浏览的一句总结**：该文把“视觉 token 参与深层全部计算”这条默认假设打破了，给出一条可实操的低成本高效率 multimodal 改造路径。

## 标准化研究框架
- **Research question：** 能否通过层级饱和特征识别，仅在晚层融合视觉信息，从而减少计算且不显著损失 multimodal 性能？
- **Literature：** 对齐 MLLM 架构优化与高效推理路线，特别是 token 选择、层间路由与 late-fusion 设计。
- **Theory：** 可视为浅层/深层语义需求的机制假设：视觉信息不需要始终走满深层语义网络。
- **Hypotheses：** 视觉 token 在中层后可近似饱和，将其转入轻量侧支并晚融合，可节约计算并保持性能。
- **Method：** 对 LLaVA-1.5 做层级注意力统计与对照实验，构建 DPVR-LF 路由策略，与标准多模态模型进行基准比较。
- **Data and Analysis：** 使用论文公开的标准 multimodal benchmark，统计吞吐、参数规模、视觉注意力退化趋势、任务指标差异。
- **Findings：** 结果支持晚融合策略在效率-性能曲线上优于全程对称处理，且未观察到明显准确率坍塌。
- **Conclusion：** 对高成本 MLLM 服务具有直接工程意义，后续可在更多模型架构上推广该路由思想并加入动态饱和检测。
