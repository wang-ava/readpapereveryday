# PAC-MAN: Perception-Aware CBF-RL for Whole-Body Safety in Humanoid Dodgeball

Spotlight：`PAC-MAN` 在 humanoid dodgeball 任务中用“感知受限、球体分割深度”替代特权位姿观测，并用 Whole-body control barrier 约束+对抗运动先验训练策略，展示了端到端可迁移到真实机器人、且无额外微调的安全躲避能力。

- 论文标题：PAC-MAN: Perception-Aware CBF-RL for Whole-Body Safety in Humanoid Dodgeball
- 作者：Lizhi Yang, Junheng Li, Aaron D. Ames
- 机构（如可得）：arXiv 页未直接给出完整机构信息
- 发布时间：2026-07-30（v1）
- 主题标签：`#EmbodiedAI` `#Humanoid` `#Robotics` `#CBF` `#ReinforcementLearning`
- 论文链接：[https://arxiv.org/abs/2607.28623v1](https://arxiv.org/abs/2607.28623v1)
- PDF 链接：[https://arxiv.org/pdf/2607.28623v1](https://arxiv.org/pdf/2607.28623v1)
- 项目/代码/数据链接：[@Project Page](https://lzyang2000.github.io/perceptive_cbf_rl/)

## 核心问题
在真实部署约束下，humanoid 要在仅依赖机载感知的情况下避障，如何同时保证全身各部位安全和动作自然性？传统依赖特权状态的方法很难直接迁移到真实硬件。

## 方法概要
方法在训练时使用 CBF（Control Barrier Function）在奖励中注入全身碰撞清晰度约束，构建每个身体连杆到球体的 clearance barrier；同时引入 Joint-CBF 与 Link-CBF 两种设置并用对抗运动先验约束动作风格。部署阶段输入仅为头部 RGB-D 的球体分割掩码深度，采用固定相机或配套 gimbal 两种感知模式。最终在 Unitree G1 上无微调直接执行 zero-shot。

## 主要贡献
- 将 CBF 安全约束与感知约束联合，形成可落地的 perception-aware 安全策略。
- 用全身 link-level CBF 替代仅躯干约束，显著提升对复杂接触姿态的躲避能力。
- 给出真实机器人硬件闭环实验（Unitree G1）与模拟 benchmark 的一致性对比。

## 关键实验或结果
- 在任意抓球抛掷 benchmark 中，策略在真实机上实现 19/20 次躲避成功（95%），0 次跌倒。
- 结果显示 Joint-CBF 需要可观测的球状态；在固定观测受限下，Link-CBF 更稳健。
- 语义分割后的球形状掩码使策略具备跨球种类的迁移能力。

## 适合关注的原因
该工作兼顾安全控制理论与可落地部署，特别适合关注 sim-to-real、具身 AI 安全约束与硬件上限的读者。它展示了即使在“信息极端压缩”感知条件下，也能通过结构化奖励实现接近 oracle 的真实性能。

## 局限性或待验证点
- 当前实验场景聚焦 dodgeball，任务分布单一。
- 无障碍多目标互动和多人协作场景尚未覆盖。
- 文章未给出大规模长时序鲁棒性统计，可能存在特定轨迹分布偏差。

## 对后续研究/应用的启发
- 可将该框架迁移到工厂协作、物流避障等部署端感知受限的机器人任务。
- 建议结合在线状态估计器，减轻 Joint-CBF 对观测缺失的敏感性。
- 可作为安全 RL 与人类风格动作先验融合范式的可复用模板。

## Obsidian 快速浏览总结
一句话：`PAC-MAN` 证明了 humanoid 即便在“只看球体分割深度”的低信息条件下，也可通过 CBF+策略先验实现高成功率的真实硬件避球。

## 标准化研究框架
- **Research question：** 如何在受限机载感知下实现 humanoid 的全身安全避障，并保持真实硬件可迁移性？
- **Literature：** 关联控制 Barrier Function、安全控制（Safe RL）、sim-to-real 具身系统，强调从 simulation 到 hardware 的连续性。
- **Theory：** 假设通过在训练奖励中编码 Link-level 的几何安全约束，可诱导策略在部署时自然满足碰撞安全。
- **Hypotheses：** 在同等条件下，固定机载分割深度输入下 Link-CBF 应优于单躯干约束，且对未知球形态泛化更强。
- **Method：** 训练时采用 CBF 指导的 reward shaping，加入对抗运动先验，推理时维持与训练一致的安全约束形式，并在模拟 benchmark 与 Unitree G1 上比较。
- **Data and Analysis：** 使用 single-throw 与 deployment loop 两类测试；记录成功率、跌倒率、不同感知模式（固定相机/跟踪云台）下策略差异。
- **Findings：** 在实验中 achieved 95% 成功率，证明了低带宽视觉表示结合 CBF 约束的实用价值。
- **Conclusion：** 对具身 AI 来说，这是一种在安全关键场景下兼顾可部署性与控制可解释性的路线，但仍需扩展到更复杂交互任务。
