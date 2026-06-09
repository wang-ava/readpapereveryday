Semantic Horizons 值得看，不是因为它又提出一个新的 prompting 技巧，而是因为它试图回答一个更基本的问题：为什么 foundation-model-guided embodied agents 一旦任务变长就会系统性掉性能。

# Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning

## 基本信息

- 论文标题：Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning
- 作者/机构：Siddharth Karuturi、Kaustubh S. Bukkapatnam；Illinois Mathematics and Science Academy
- 发布日期或版本日期：2026-05-27（OpenReview）；最后修改 2026-06-02
- 主题标签：#EmbodiedAI #Planning #Theory #FoundationModels #InformationTheory
- 论文链接：https://openreview.net/forum?id=CNej21yr6r
- PDF 链接：https://openreview.net/pdf?id=CNej21yr6r
- 项目链接：未见公开项目页
- 代码链接：文中称 acceptance 后公开
- 数据链接：文中验证覆盖 ALFRED、RLBench、Habitat、MetaWorld

## 核心问题

foundation models 在 embodied tasks 上常见的失败模式是：短任务还行，任务 horizon 一长就明显下滑。社区已经提出 chain-of-thought、hierarchical planning、adaptive replanning 等经验方法，但为什么会掉、掉到哪里、什么量在控制上限，缺乏统一解释。本文要回答的是：能否给 foundation-model-guided planning 的最大可靠 horizon 建立一个理论边界？

## 方法概要

作者提出 Planning Information Bottleneck（PIB），用一个标量 \(B\) 来度量 VLM 把物理观察压缩成内部表征时不可恢复地丢失了多少任务相关信息。基于这个量，论文推导出四个理论结果：Semantic Horizon Theorem、Optimal Subgoal Count、Adaptive Replanning Criterion，以及 Calibration-Bottleneck Duality。随后在多种 VLM/VLA 与 embodied benchmarks 上验证这些公式的预测力。

## 主要贡献

- 提出 PIB 这一统一量化视角，把长时 planning 失败解释为信息瓶颈问题。
- 给出第一个关于最大可靠 planning horizon 的闭式理论界。
- 推导最优 subgoal 数量与何时应 replanning 的理论条件。
- 提出 PIB-AUC，作为预测长时失败风险的新评估维度。

## 关键实验或结果

- 论文在五个模型上验证理论，包括 LLaVA-1.6、GPT-4V、Gemini-1.5-Pro、InternVL2、OpenVLA。
- benchmark 覆盖 ALFRED、RLBench、Habitat、MetaWorld。
- 文中报告理论 horizon 预测与经验测量的误差约在 8.7% 以内。
- 相关性给到 \(r = 0.991\)，并报告 \(p < 10^{-16}\)，说明理论量与实际长时失败高度一致。
- PIB-AUC 对 long-horizon failure 的预测能力比现有 VQA-based 分数高约 2 到 5 倍。

## 适合关注的原因

如果你正在做 embodied planning、agent evaluation、VLA reliability 或 hierarchical control，这篇很有价值，因为它试图把“经验上知道任务长会坏”上升到可量化理论。哪怕你不同意其具体公式，这类工作也会推动大家用更 principled 的方式讨论 horizon、subgoal 与 replanning。

## 局限性或待验证点

- 目前是 workshop/poster 级公开版本，理论是否能稳定覆盖更多模型家族仍需后续检验。
- PIB 作为单一标量可能压缩了过多细节，不同模态瓶颈是否都能统一进同一量仍值得讨论。
- 论文虽在多个 benchmark 上验证，但现实机器人中的感知噪声、执行误差与安全约束会带来额外偏差。
- 代码和完整实验资产尚未公开，只说明 acceptance 后释放。

## 对后续研究/应用的启发

后续研究可以围绕 PIB 设计更好的 state abstraction、subgoal decomposition 和 replanning triggers，而不是只靠 prompt engineering 调参。应用上，这种理论指标如果成熟，可直接用于任务分解、风险预估和何时交回人类控制的阈值设定。

## Obsidian 快速浏览总结

这篇论文把 embodied foundation model 的“长任务掉线”问题，首次较系统地写成了一个信息瓶颈与 horizon 上界问题。

## 标准化研究框架

**Research question：** 本文研究的问题是：foundation model 引导的 embodied agent 为什么会随任务 horizon 增长而失效，以及这种失效能否被一个统一理论量刻画。

**Literature：** 相关文献包括 embodied planning、hierarchical planning、adaptive replanning、VLM/VLA evaluation 与信息论式表示瓶颈分析。本文尝试把这些分散经验统一到 planning information bottleneck 框架下。

**Theory：** 这是本文最核心的部分。作者提出 PIB，认为任务相关信息在 observation-to-representation 压缩中的不可恢复损失，决定了最大可靠 planning horizon、最优 subgoal 密度和 replanning 触发条件。

**Hypotheses：** 可等价理解为：如果 PIB 确实捕获了 foundation model 内部压缩造成的关键信息损失，那么它应能高精度预测长时任务中的失败边界，并优于现有经验评估指标。

**Method：** 方法上先从信息论推导 Semantic Horizon、Optimal Subgoal Count、Adaptive Replanning 和 Calibration-Bottleneck Duality，再在多模型多 benchmark 上做经验验证。

**Data and Analysis：** 数据与分析覆盖五个 foundation models 和四个 embodied benchmarks，比较理论预测与实测 horizon、失败率和评估指标之间的吻合程度，并提出 PIB-AUC 作为新指标。

**Findings：** 主要发现是 PIB 对最大可靠规划长度和长时失败具有很强预测力，理论预测与经验结果高度相关，并能比现有 VQA-style 评估更好预判 long-horizon breakdown。

**Conclusion：** 结论是 embodied foundation models 的长时失败并非纯工程偶然，而与表征压缩带来的信息瓶颈密切相关；future planning systems 应显式围绕 horizon、subgoal 和 replanning 做信息预算设计。
