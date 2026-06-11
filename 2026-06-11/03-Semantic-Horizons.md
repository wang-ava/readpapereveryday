# Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning

这篇论文把“embodied agent 为何会长时失败”从经验观察变成信息论边界问题：通过 PIB（Planning Information Bottleneck）给出可计算的规划视界，直接解释了 horizon 失效的根因。

## 基本信息

- 论文标题：Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning
- 作者/机构（如可得）：Siddharth Karuturi、Kaustubh S. Bukkapatnam（机构信息未在页面展开，需后续从 PDF/附录确认）
- 发布日期或版本日期：2026-05-27（发布），6-day 内最新修订：2026-06-02
- 主题标签：#EmbodiedAI #InformationTheory #VLM #VLA #Planning #LLM
- 论文链接：https://openreview.net/forum?id=CNej21yr6r
- PDF 链接：https://openreview.net/pdf?id=CNej21yr6r
- 项目/代码/数据链接（如可得）：当前页仅提及将发布；未给出明确链接。

## 核心问题

现有 embodied planner 在任务长度增加时快速退化明显，但缺乏统一解释。问题在于：VLM/VLA 在表示压缩阶段不可避免丢失任务相关信息，导致 horizon 增大后误差累积。

## 方法概要

论文定义 PIB 标量 B（bits）表示状态信息到动作的可决策信息损失，基于 Fano 不等式推导长时可靠规划上界。作者据此得到 semantic horizon、最优子目标数、重规划阈值和校准-瓶颈关系等四个结果，并通过 PIB-AUC 进行跨 horizon 评估。

## 主要贡献

- 首次将 PIB 引入 embodied foundation model planning，提供可计算规划视界闭式上界。
- 给出最优子目标数量和动态重规划条件的理论公式。
- 提出 PIB-AUC，作为比传统 VQA 式评分更有预判力的失败预测指标。
- 在 ALFRED、RLBench、Habitat、MetaWorld 上以实证回归验证理论常数与拟合度。

## 关键实验或结果

文中报告在五个模型与四个基准上，理论预测与经验上界的偏差较小，相关度高（r=0.991）；PIB-AUC 在长时失败预测上明显优于已有指标。定量增强了“为何长时规划系统必须控制瓶颈”的工程依据。

## 适合关注的原因

相比经验式调参，这篇工作提供了可解释的设计建议：什么时候该拆子目标、什么时候该重规划、如何设置信赖度阈值。对于 Agentic VLA / Robot control pipeline 这类系统，能直接影响部署安全性。

## 局限性或待验证点

- 数据主要来自公开 benchmark，仍需真实机器人平台与领域任务外推。
- PIB 与任务空间近似下界依赖建模假设，边界松紧需跨域验证。
- 代码/数据版本是否对齐最新修订，需追踪后续官方发布。

## 对后续研究/应用的启发

可把 PIB 用作“任务计划控制面板”指标：在任务分解器、子目标选择器和 replanning module 之间形成统一控制闭环；对跨任务迁移也更有解释性。

## Obsidian 快速浏览总结

该文把“长时失败”从经验规律升级为有理论上界可计算的设计问题，是 embodied agent 方向的一次重要可解释性升级。

## 标准化研究框架

**Research question：** 在 VLM/VLA 指导下的 embodied planning 中，任务相关信息瓶颈 B 能否定量预测可靠 horizon，并指导 subgoal 与 replanning 设计？

**Literature：** 关联了 embodied planning、information bottleneck、VLM/VLA 控制流水线三类文献，补足了缺少硬理论上界的空缺。

**Theory：** 论文核心是信息论推导：PIB 作为任务相关可决策信息的损失指标，进而导出 success-upper-bound 与 replanning 条件。

**Hypotheses：** 对应假设为：可用 PIB 估计决策可靠 horizon，并据此设定 subgoal 数与阈值。与社会科学里统计假设检验不同，这里是“在可观测变量变换下的上界/校准命题”。

**Method：** 先定义 PIB，推导四项定理，再在 benchmark 上估计 PIB，最后对比 PIB-AUC 与传统指标。

**Data and Analysis：** 选择 LLM/VLM/VLA 基线与 4 个仿真环境，对不同 horizon 下 success 与指标变化拟合，统计相关性与偏差。

**Findings：** 实验支持 PIB 上界与经验结果高度一致，且 PIB-AUC 对长时失败预测更优。

**Conclusion：** 该框架对长时 embodied 系统有直接可落地的指导价值；后续应扩展至真实物理机器人与多任务交叉域验证。
