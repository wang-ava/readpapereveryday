# SSM-PixNav: State Space Models for Pixel-Guided Embodied Navigation

SSM-PixNav 关注“像素级目标导航”的高精度问题，把 RGB 与 depth 的时序信息整合进更轻量的 SSM 策略中。它直接针对真实部署中最要命的效率瓶颈，给出能在复杂导航任务里维持精度的替代方案。  
与传统 transformer 主导的像素导航范式相比，这项工作强调用可复现基准和轻量时序建模同时改进训练稳定性和推理成本。

- **论文标题**：SSM-PixNav: State Space Models for Pixel-Guided Embodied Navigation  
- **作者/机构**：Athira Krishnan R, Sumohana S. Channappayya（机构信息在 OpenReview 页面未公开）  
- **发布日期/版本日期**：2026-06-10（v1）  
- **主题标签**：#EmbodiedAI #Navigation #RobotLearning #StateSpaceModel #CV  
- **论文链接**：<https://openreview.net/forum?id=RmsMd5vdBf>  
- **PDF 链接**：<https://openreview.net/pdf?id=RmsMd5vdBf>  
- **项目/代码/数据链接（如可得）**：  
  - 代码与数据集：<https://github.com/lfovia/SSM-PixNav>  
  - 数据集：RGBD-PixNav（使用 HM3D scenes in Habitat-Sim 构建）  

- **核心问题**：在 pixel-goal navigation 中，传统方法多依赖 RGB，缺少深度几何线索，导致“像素定位正确但行驶路径不可靠”；同时 transformer 方法参数量高，不适合资源受限系统。  
- **方法概要**：  
  1. 提出 RGBD-PixNav，将 RGBD 作为统一任务输入。  
  2. 用 Mamba 型 State Space Model（SSM）替代重型 transformer，提升时间建模效率。  
  3. 设计 depth-gating 机制，在不同场景下自适应融合 RGB 与 depth。  
  4. 构建可复现实验用的 PixNav Trajectories 数据集与标准训练/验证切分。  
- **主要贡献**：  
  1. 将 pixel-goal 导航问题升级为可完整复现实验任务，不再停留在少数演示基准。  
  2. 在同类任务中给出更轻量的时序模型路线，参数规模约 27M。  
  3. 通过 depth-gating 提升在视觉近似场景中的可辨识性，缓解误导。  
- **关键实验或结果**：  
  - Causal SSM-RGB 和 RGBD 变体在成功率上均优于 strong baselines，提升约 0.4。  
  - 参数量约为 27M，约为部分对比方法的一半。  
  - 在观测噪声和历史长度变化下均表现出更稳健的导航成功率。  
- **适合关注的原因**：  
  1. 像素级导航是 embodied 场景里非常真实且难度高的任务定义。  
  2. 数据集和代码可复现性较完整，方便做 baseline 对比。  
  3. 模型轻量化与效果兼顾，适合资源受限机器人平台。  
- **局限性或待验证点**：  
  1. 主要评测在 HM3D 场景内，真实世界部署仍有域迁移风险。  
  2. 论文未披露极端动态遮挡下的长期行为稳定性上界。  
  3. 多智能体与多任务协作场景尚未覆盖。  
- **对后续研究/应用的启发**：  
  可以将 RGBD-PixNav 与策略安全约束、能耗约束联合，测试在移动平台和 service robot 里可落地的轻量导航模型路径。  
- **Obsidian 快速浏览的一句总结**：SSM-PixNav 用更轻量的时序建模与深度门控，显著提升像素目标导航精度和部署友好性。  

## 标准化研究框架
- **Research question：** 如何在像素级目标导航中，在保障精度的同时降低模型计算开销并提高部署可复现性？  
- **Literature：** 以往 pixel-goal、目标导航与视觉导航方法偏重 transformer 或单模态视觉，本工作在此基础上补充了 state-space 与 depth 融合。  
- **Theory：** 将时序决策建模为受控状态空间过程，并通过深度可控门控提高几何相关特征权重。  
- **Hypotheses：** 若将 depth 作为主动控制信号并采用 SSM 时序骨干，可在保持精度的同时显著压缩参数与计算成本。  
- **Method：** 构建 RGBD-PixNav 任务定义和数据切分，用 Mamba-SSM 与 depth-gating 做端到端训练，比较 Causal SSM-RGB 与 Causal SSM-RGBD。  
- **Data and Analysis：** 用 HM3D/Habitat-Sim 构建轨迹库，并在成功率、历史长度敏感性和噪声鲁棒性上做 ablation 与 baseline 对比。  
- **Findings：** 结果显示轻量 SSM 模型可在保持或超越基线表现的前提下显著省模型参数，并对噪声更稳健。  
- **Conclusion：** 对非社会科学研究，这一框架可理解为“任务定义-数据标准化-轻量时序模型联合优化”；价值在于把复杂 embodied 导航问题变成可复现、可迭代的工程研究线。  
