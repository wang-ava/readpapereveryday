# FurnitureVLA：真实尺度双臂装配的长期任务新基准

FurnitureVLA 是当前少有从真实世界尺度、长时序、双臂协作角度系统化建模的 VLA 工作之一，覆盖了“模拟到真实”的关键闭环。它对我们理解长时序具身系统如何稳定从子任务过渡非常有价值。

- 论文标题：FurnitureVLA: Learning Long-Horizon Bimanual Furniture Assembly with Vision-Language-Action Model
- 作者/机构（如可得）：Chenyang Ma, Yue Yang, Radu Corcodel, Siddarth Jain, Andrew Wu, Chiori Hori, Diego Romeres；机构：Mitsubishi Electric Research Laboratories（MERL）, University of Oxford, UNC Chapel Hill
- 发布日期或版本日期：2026-07-01（Submitted on 1 Jul 2026，v1）
- 主题标签：#EmbodiedAI #Robotics #VLA #LongHorizon
- 论文链接：[https://arxiv.org/abs/2607.01212](https://arxiv.org/abs/2607.01212)
- PDF 链接：[https://arxiv.org/pdf/2607.01212v1.pdf](https://arxiv.org/pdf/2607.01212v1.pdf)
- 项目/代码/数据链接：
  - 项目页：[https://dannymcy.github.io/furniturevla/](https://dannymcy.github.io/furniturevla/)
  - 代码：当前页面主要提供项目与演示信息，未在快照中出现独立公开代码仓库链接

- 核心问题：现实尺度家具装配通常长期、双臂交互复杂，并且容易在长序列中积累错误；现有方法多停留在玩具级/单臂。如何构建真实装配任务基准并提升 VLA 长时程稳定性？
- 方法概要：定义真实家具装配任务及 12–25 技能序列，搭建模拟数据生成与评估流水线，并构建 VR 远程标注系统采集高质量演示。提出 progress-enhanced VLA，在语义子任务上微调，联合预测控制动作与连续 progress 信号，实现子任务自动切换。
- 主要贡献：
  1. 系统化发布第一类真实尺度双臂装配任务定义与基准框架。
  2. 将 progress 信号引入 action 生成以降低长时序 compounding error。
  3. 对模拟与真实 Kinova Gen3 的端到端评测给出对照，支撑 sim-to-real 分析。
- 关键实验或结果：模拟任务中平均成功率从 48% 提升到 80%，设计因素研究再带来约 21% 增益；在最难任务上由模拟到真实的性能仅出现约 16% 下降。
- 适合关注的原因：具身智能中的“多步长任务”长期是瓶颈，这篇论文给出从数据、建模、任务拆分到 sim2real 的一体化范式。
- 局限性或待验证点：
  - 公开信息中代码/预训练权重覆盖度有限，外部复现实验仍依赖论文附录与项目同步更新。
  - 任务聚焦家具装配，跨家居之外领域（厨房、仓储）泛化有待验证。
- 对后续研究/应用的启发：进展信号可作为 generalizable trajectory governance 的一种简洁替代，不一定需要复杂 planner，即可显著减少长任务中的失控扩散。
- 一句适合 Obsidian 快速浏览的中文总结：FurnitureVLA 的价值不只是装配表现，而在于把 progress-aware 子任务切换嵌入动作模型，系统性提升长程具身行为稳定性。

## 标准化研究框架
**Research question：** 在真实世界双臂、长时程任务里，VLA 能否通过进度信号与语义子任务建模缓解动作累积误差？

**Literature：** 传统机器人装配与 LLM-based policy 通常分离处理 perception/action 与计划。该研究的等价思路是把 progress 作为显式状态变量，与控制统一学习。

**Theory：** 长时序任务中的误差主要源于状态漂移；若模型能持续预测“执行进度”，可在决策时触发子任务切换，抑制错误传播。

**Hypotheses：** 语义子任务监督 + 连续 progress 信号可提高长序列任务成功率，并提升 sim2real 保真性。

**Method：** 设计双臂装配基准、VR 采集示范、sim pipeline 与 real Kinova 部署；对比基线与 progress-enhanced VLA 的成功率与鲁棒性。

**Data and Analysis：** 使用三类家具任务（LACK、KALLAX、IVAR）与多步长子任务数据，评测 sim 与 real 的成败差异和错误恢复行为。

**Findings：** 进度增强策略显著改善长时程成功率，并能降低 sim 到真实系统的退化。

**Conclusion：** 该研究支持“进度导向的行为建模”在具身长时序问题中的有效性，可成为 VLA 线下到线上迁移的关键接口。
