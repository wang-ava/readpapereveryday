---
spotlight: "这项工作把控制从“重训模型”移到了“激活空间干预”，为 CV 系统提供了更轻量也更可解释的风格与概念控制方式。"
---

# AcFlow: Controlling Text-to-Image Diffusion Transformers via Learned Conditional Activation Flow

## 基本信息
- **论文标题**：AcFlow: Controlling Text-to-Image Diffusion Transformers via Learned Conditional Activation Flow
- **作者**：Junran Wang, Zehao Jin, Tianyu Luan, Xinjie Shen
- **机构**：arXiv 页面未公开。
- **发布日期 / 版本日期**：2026-09-09（v1）
- **主题标签**：`CV` `Text-to-Image` `Diffusion` `Activation Control` `Inference-time` `Generative`
- **论文链接**：https://arxiv.org/abs/2609.10723
- **PDF 链接**：https://arxiv.org/pdf/2609.10723
- **项目/代码/数据链接**：代码仓库：https://github.com/Nove1yst/AcFlow

## 核心问题
在保持基座 DiT 不变的前提下，如何让文本到图像生成在风格和概念抑制上更精细可控？传统提示词控制在复杂约束下常失效，而全量微调成本高。

## 方法概要
论文提出 AcFlow：
- 在推理阶段学习条件激活流（conditional activation flow）；
- 利用文本概念描述构造目标速度场；
- 在中间层 token activation 上施加状态相关更新；
- 通过积分步长控制风格/抑制强度。

方法的关键在于：基座模型冻结，只新增一个可复用的流函数模块，实现跨概念泛化。

## 主要贡献
- 将控制问题下沉到激活空间（activation space）而非输入空间 prompt 优化。
- 证明单模块可覆盖风格与概念抑制多任务，无需逐概念再训练。
- 保持生成模型核心参数不变，适合部署在算力敏感场景。

## 关键实验或结果
- 风格控制上达到 `0.5365 / 0.2860` 的 style-content balance，优于基线 `0.4397 / 0.2684`。
- 在文本可解释概念失配和抑制任务中，AcFlow 显示更稳定的 token 级更新行为。

## 适合关注的原因
相比微调或多轮提示搜索，AcFlow 更贴近工程部署：参数冻结、推理时可解释控制、可扩展性更好，是 CV 生成与产品化 pipeline 的实用改进方向。

## 局限性或待验证点
- 评测主要聚焦于风格与概念抑制任务，复杂语义一致性长期稳定性未充分展开。
- 对极端细粒度文本指令是否仍保持同等可控性需扩展。
- 抑制能力对新兴语义类别的外推边界尚未系统给出。

## 对后续研究/应用的启发
- 可直接迁移到图像编辑或广告生成系统，实现统一控制器层。
- 通过共享一个流模块支持不同任务风格，适合做低成本“风格策略库”。
- 可尝试与扩散蒸馏结合，进一步压缩推理时延。

## 一句话中文速览总结
AcFlow 用推理时激活流把控制从重训练改为可复用的参数轻量注入，既保留基模型能力又提升文本控制质量。

## 标准化研究框架
- **Research question：** 在不重训基座模型的前提下，能否通过条件化激活流提升文本到图像的风格/概念控制？
- **Literature：** 现有控制方法偏重 prompt 工程或 finetune，灵活性和代价存在权衡。
- **Theory：** 激活流可把目标概念作为控制场嵌入采样轨迹，实现 token 级、状态依赖的生成方向校正。
- **Hypotheses：**（1）固定基座+激活流可显著优于纯 prompt；（2）该方式在跨概念场景具有较好外推；（3）推理控制强度可作为独立调参维度。
- **Method：** 在 DiT 上加入条件激活场网络，基于概念文本训练速度场并固定基底参数，在多基线下做风格与抑制对比。
- **Data and Analysis：** 使用公开风格与抑制任务，比较 style-content trade-off 指标和定性场景；评估 unseen concept 泛化。
- **Findings：** AcFlow 在风格对齐和抑制任务上取得更优折中，保持了基座结构的泛化能力。
- **Conclusion：** 该框架为低代价推理控制提供了有前景路径，但在更复杂语义任务中的长期一致性仍有待验证。
