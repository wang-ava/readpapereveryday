> **Spotlight：** $\omega$-0 用一个潜变量 world-action model 同时处理移动、姿态、平衡与操作，并以未来观察 embedding 预测取代昂贵的视频重建。它把“看见未来”和“生成可执行全身动作”压进同一控制框架。

# $\omega$-0: A Latent Predictive World Action Model for Concurrent Humanoid Loco-Manipulation

- **作者/机构：** Zhe Li、Zhenzhe Zhang、Yangyang Wei、Wenjie Zhang、Xichen Yuan、Peiyuan Zhi、Gen Li、Xinying Guo、Fengjie Gao、Jianfei Yang、Shanghang Zhang；机构待正文核对
- **发布日期/版本：** 2026-08-06，arXiv v1
- **主题标签：** #具身智能 #人形机器人 #WorldModel #VLA #DiffusionPolicy #机器人学习
- **论文链接：** https://arxiv.org/abs/2608.06375
- **PDF：** https://arxiv.org/pdf/2608.06375
- **项目/代码/数据：** 摘要页未提供公开项目、代码或 $\omega$-HOME 下载链接

## 核心问题

家庭任务常要求人形机器人一边移动一边操作物体，同时协调姿态与平衡。传统系统把 locomotion 和 manipulation 拆开，容易形成接口瓶颈；已有 world-action model 又多偏向机械臂或视频生成，难以直接输出全身可执行控制。

## 方法概要

$\omega$-0 接收语言指令、当前视觉观察和机器人本体状态，直接预测与控制器兼容的 whole-body action latents。它不重建完整未来视频，而是预测紧凑的未来观察 embedding，以轻量预测目标学习视觉前瞻，再用 diffusion-based action generation 产生全身动作。系统支持第一视角 RGB、第三视角 RGB 和第三视角深度，并通过 controller-based simulation replay 将人类/公开视觉运动先验落到机器人可执行动作空间。

## 主要贡献

1. 提出面向真实人形机器人 concurrent loco-manipulation 的潜预测 whole-body world-action model。
2. 用未来 embedding 预测耦合视觉前瞻与扩散动作生成，避免把高成本像素重建当作唯一世界建模目标。
3. 收集 **$\omega$-HOME**：40+ 小时真实家庭数据，含同步多视角观察、whole-body SMPL motion、机器人状态与动作潜变量。
4. 用单一模型覆盖 11 项家庭任务，并与 imitation learning、VLA、humanoid policy 和 WAM 基线比较。

## 关键实验或结果

官方摘要称，单个 $\omega$-0 在 11 个真实家庭任务上能生成平滑的“边移动边操作”行为，并持续优于代表性 imitation learning、VLA、humanoid 和 WAM 基线。公开摘要没有给出各任务成功率、试验次数、误差条或失败类型，因此目前只能确认方向性结论，不能判断优势幅度和统计稳健性。

## 适合关注的原因

论文把人形机器人控制从模块串联推进到统一的预测—行动潜空间，并提供规模可观、模态同步的数据集描述。更重要的是，它提出一个值得验证的工程判断：对控制而言，预测未来表征可能比生成未来像素更高效、更贴近动作需求。

## 局限性或待验证点

- 11 个家庭任务的物体、场景扰动和长尾失败覆盖范围需看正文；“真实世界”不等于开放世界泛化。
- 潜空间预测可提升效率，但可能掩盖碰撞、接触和细小物体状态等控制关键细节。
- controller-based replay 依赖控制器与仿真质量，sim-to-real 偏差可能被转移而非消除。
- 数据、代码和项目页在摘要页尚不可得，复现性暂时有限。

## 对后续研究/应用的启发

可以系统比较三类预测目标：像素未来、语义未来 embedding、接触/动力学状态未来，检验哪类对不同操作任务最有效。还可为潜动作加入安全约束或 uncertainty head，在平衡风险上升时自动降速、重规划或切换保守控制器。

## Obsidian 快速浏览总结

**一句话：$\omega$-0 以未来表征预测联合全身扩散控制，让人形机器人不再先走到位再操作，而是学习真正的边走边做。**

## 标准化研究框架

**Research question：** 能否用统一 world-action model 实现真实人形机器人稳定的并行移动与操作？

**Literature：** 工作位于 humanoid locomotion、imitation learning、VLA 与 world-action model 的交叉点，针对运动/操作分解和机械臂中心化局限。

**Theory：** 等价理论主张是，紧凑未来观察表征足以提供控制相关的视觉前瞻，并可与全身动作潜空间共同学习。

**Hypotheses：** 非社会科学假设检验；技术假设是联合潜预测策略优于分解式策略及视频重建导向 WAM，并能跨多视角输入工作。

**Method：** 多模态状态编码、未来 observation embedding 预测、diffusion-based whole-body action generation，以及控制器仿真回放对齐。

**Data and Analysis：** $\omega$-HOME 40+ 小时同步真实数据；11 项家庭任务；对比 imitation learning、VLA、humanoid 与 WAM 基线。

**Findings：** 摘要报告单模型可生成平滑 concurrent loco-manipulation，并在受测任务上持续超过基线；绝对数字待正文核对。

**Conclusion：** 面向人形机器人的 world-action model 可围绕控制相关潜未来建模，而不必依赖完整视频重建或运动—操作分解。

