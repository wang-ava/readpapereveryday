# Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning

这篇论文最值得跟踪的点是它把“embodied 长时失败”从经验现象升级为可计算可度量的理论量，让 long-horizon planning 有了量化边界。 

## 基本信息

- 论文标题：Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning
- 作者/机构（如可得）：Siddharth Karuturi；Kaustubh S. Bukkapatnam（未在入口页展开完整机构信息）
- 发布日期或版本日期：2026-05-27（OpenReview）；Last Modified 2026-06-02
- 主题标签：#EmbodiedAI #InfoTheory #Planning #VisionLanguageAction #LongHorizon
- 论文链接：https://openreview.net/forum?id=CNej21yr6r
- PDF 链接：https://openreview.net/pdf?id=CNej21yr6r
- 项目/代码/数据链接（如可得）：
  - 代码：未见公开代码链接
  - 数据：使用 ALFRED、RLBench、Habitat、MetaWorld 做 benchmark 验证（公开任务套件）
  - 项目页：未见独立项目页

## 核心问题

为什么 foundation model 引导的 embodied agent 在任务步数增长时会系统性失效？是否能定义可计算指标来预测可持续规划长度和最优任务分解？

## 方法概要

作者引入 Planning Information Bottleneck（PIB）标量 B，表示 VLM 对物理观测进行 task-relevant 压缩时不可恢复信息损失。基于 B 推导
a) 语义规划上界（Semantic Horizon）；b) 最优 subgoal 数；c) adaptive replanning 判据；d) calibration 与瓶颈的对偶关系。 

## 主要贡献

- 给出了 embodied planning 的首个“理论上界”框架：可把 long-horizon 失败归因于可恢复信息容量不足；
- 通过 PIB 统一任务长度、复杂度与重规划策略；
- 引入 PIB-AUC 作为长时评估指标，强调验证早于经验式 VQA 分数。

## 关键实验或结果

- 在五类 VLM/VLA 上、四个 benchmark 上验证理论预测。
- 报道 PIB 预测误差约 8.7%，与经验测量相关性 r=0.991，p < 10^-16。
- PIB-AUC 对长时失败预测能力明显优于既有 VQA 型分数（约 2–5 倍）。

## 适合关注的原因

许多团队都在做更强模型和更大轨迹，但缺少 failure budget 的统一定义。该工作把“模型更大就能更长跑得更久”这种经验预设形式化为可对照、可验证、可做系统对比的量化框架。 

## 局限性或待验证点

- 论文为理论导向，跨不同 embodiment 和真实硬件场景的外推还需更多实证；
- PIB 是单一标量，可能压缩了多模态误差来源（感知噪声、执行抖动、动作精度）；
- 代码与实现细节公开程度决定了不同任务迁移的可复现性。

## 对后续研究/应用的启发

- 在 agent 里可把 PIB 作为安全阈值：当接近语义 horizon 时自动分解子目标或降级为更保守策略；
- 该框架可作为 planning benchmark 的统一对齐指标，与成功率/回报并行报告。 

## Obsidian 快速浏览总结

一句话：它把 long-horizon embodied 失败用信息论做成可量化约束，适合直接指导 planning policy 的分段与 replanning 设计。

## 标准化研究框架

**Research question：** 可否用可恢复任务信息量（PIB）预测并限制 foundation model-guided embodied planning 的可靠 horizon？

**Literature：** 与传统 purely empirical 的 planning benchmark 不同，本论文连接 information bottleneck 与 embodied failure，接近可解释 AI 与控制理论的交叉线；也与 existing 经验式 VQA 指标形成对比。 

**Theory：** 论文的核心理论就是 PIB：任务相关信息在状态压缩过程中的不可恢复损失决定规划上界。该框架可类比为“信息预算理论”，不直接套用社会科学假设检验。 

**Hypotheses：** 等价表述为：PIB 可单调解释 horizon 上限与模型失效点；若 PIB 高则长时成功率下降，且通过 PIB-AUC 可更早预警失败。 

**Method：** 在同一 benchmark 下，测量不同模型/任务的观察压缩与 success 曲线，用 PIB 推导 horizon、subgoal 数与 replanning 阈值并与实测对齐。 

**Data and Analysis：** 数据包含 ALFRED、RLBench、Habitat、MetaWorld 等多任务；分析对比理论曲线与实测 long-horizon 失效概率，并比较 PIB-AUC 与历史指标。 

**Findings：** 在公开数据上，理论预测与实测高度匹配（r=0.991），PIB-AUC 在 long-horizon failure 预测上更优。 

**Conclusion：** 该理论为 embodied planning 提供可执行诊断信号；但要走向工程落地还需在真实机器人和多模态噪声下扩展验证。 
