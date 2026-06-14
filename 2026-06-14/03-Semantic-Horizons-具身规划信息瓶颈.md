# Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning

Semantic Horizons 从信息论角度给出 VLM/VLA 的“可规划视距”上限，提供了可计算的 planning horizon 与子目标密度准则，为具身智能的长链条任务建立了可验证的理论瓶颈。

- **论文标题**：Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning
- **作者/机构**：Siddharth Karuturi, Kaustubh S. Bukkapatnam（论文主页未统一列出完整机构）
- **发布日期/版本日期**：2026-06-02（Published: 27 May 2026, Last Modified: 02 Jun 2026, FMEA @ CVPR 2026）
- **主题标签**：#EmbodiedAI #VLM #VLA #Theory #Planning #InformationTheory
- **论文链接**：<https://openreview.net/forum?id=CNej21yr6r>
- **PDF 链接**：<https://openreview.net/pdf?id=CNej21yr6r>
- **项目/代码/数据链接（如可得）**：论文中说明“代码、数据和实验工件将在接收后发布”；当前条目未见公开链接。
- **核心问题**：为何基座模型在任务 horizon 增长时，规划成功率迅速掉线？缺少“可解释、可定量”的任务视距边界。
- **方法概要**：
  1. 定义语义信息损失量 `B`（Planning Information Bottleneck）。
  2. 推出四条理论结果：
     - Semantic Horizon 定理（给出可成功规划 horizon 的上界）；
     - 最优子目标数量推导；
     - 自适应重规划门槛；
     - 校准-瓶颈对偶关系。
  3. 在 LLaVA-1.6、GPT-4V、Gemini-1.5-Pro、InternVL2、OpenVLA 上做多基准验证（ALFRED、RLBench、Habitat、MetaWorld）。
  4. 提出 `PIB-AUC` 评价指标，比较传统 VQA 型指标的长程任务预测能力。
- **主要贡献**：
  1. 首次将具身规划退化问题映射为信息瓶颈理论框架；
  2. 将 horizon、子目标数和重规划时机形式化为可计算量；
  3. 构造可泛化到多模型/多基准的评估轴 `PIB-AUC`。
- **关键实验或结果**：理论预测与经验观察偏差约 8.7%；`r = 0.991, p < 10^{-16}`，并在某些基准上显著优于传统评估在失败预警上的准确性。
- **适合关注的原因**：
  1. 为长时序具身任务提供明确“能做几步”边界，而非仅依赖经验超参；
  2. 可帮助规划模块按任务 horizon 调整子目标分解；
  3. 为具身系统稳定性和可部署性评估提供可验证度量。
- **局限性或待验证点**：
  1. 实验覆盖的基准仍局限于通用环境；
  2. 公式参数与现实噪声建模存在差距，需要更多真实机器人数据验证；
  3. 当前“接收后公开”导致复现实验资源尚未完整开放。
- **对后续研究/应用的启发**：可将 PIB 理论嵌入控制器，做“可变子目标密度 + 自适应重规划”策略，减少长任务崩坏。
- **Obsidian 快速浏览一句总结**：这篇文献把“具身 AI 做不了那么久”变成可量化公式：planning horizon 有可计算上限，关键是减少语义信息损失。

## 标准化研究框架
- **Research question：** 在 VLA/VLM 驱动的具身规划中，能否用统一的信息瓶颈指标预测成功 horizon 和子目标分解策略？
- **Literature：** 与具身 RL、VLM 控制、信息瓶颈与决策理论交汇，补足了原先“只给分数不讲失败边界”的评估空白。
- **Theory：** `B`（语义信息瓶颈）越大，任务 horizon 上限越高；引入重规划阈值可延缓误差累计。
- **Hypotheses：** 基于 `B` 和 PIB-AUC 设计的规划器比固定子目标/固定重规划策略更稳定。 
- **Method：** 计算不同模型、不同 benchmark 下 `B` 与经验成功率映射关系，拟合理论定律并进行统计显著性检验。
- **Data and Analysis：** 使用 ALFRED、RLBench、Habitat、MetaWorld 任务序列；对比传统 VLA 指标与 PIB-AUC 的任务失败预警能力。
- **Findings：** 形成了在多个 benchmark 上具备一致性的 horizon 估计能力，理论和经验一致性较高。
- **Conclusion：** 论文把具身推理从“凭经验调参”推向“有理论可检验的工程控制”，值得在真实机器人控制器中尝试。
