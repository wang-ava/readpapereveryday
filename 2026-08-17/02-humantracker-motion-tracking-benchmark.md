# HumanTracker: Towards Comprehensive and Human-Aligned Motion Tracking Benchmark

Spotlight：论文认为传统运动跟踪指标只看几何误差会遗漏人类最关注的接触稳定性与生理合理性。它以“可感知对齐”的 HumanScore 为核心，在 humanoid 运动任务中给出更贴近人类判断的 benchmark 方向。

## 论文信息
- 论文标题：HumanTracker: Towards Comprehensive and Human-Aligned Motion Tracking Benchmark
- 作者（机构）：Dairu Liu; Zekun Qi; Jiayu Zeng; Ruixi Yu; Yu Guan; Yintianrun Zhang; Xuchuan Chen; Sikai Liang; Zekai Li; Chenghuai Lin; Xinqiang Yu; Wenyao Zhang; He Wang; Li Yi（机构未在该 arXiv 摘要页完整公开）
- 发布日期：2026-08-13（v1）
- 主题标签：`#CV` `#EmbodiedAI` `#MotionTracking` `#Benchmark` `#HumanAlignment`
- 论文链接：[https://arxiv.org/abs/2608.13555v1](https://arxiv.org/abs/2608.13555v1)
- PDF 链接：[https://arxiv.org/pdf/2608.13555v1](https://arxiv.org/pdf/2608.13555v1)
- 项目/代码/数据链接：未在摘要页给出可直接链接；已声明接收 ECCV 2026，数据与基准细节待论文官方发布同步确认
- 核心问题：现有 humanoid tracking 的评估过于偏重 kinematic error，无法反映人类偏好的接触稳定、动作自然性与长序列可理解性。
- 方法概要：构建 HumanTracker benchmark，采集约 153 小时多表演者运动轨迹，加入文本化细粒度标签；定义 HumanScore 指标，通过 12K 对 24K 运动样本学习偏好，对比传统 kinematic 指标暴露差异。
- 主要贡献：
  - 提出覆盖接触、稳定性与感知偏好的综合评估框架。
  - 构造大规模细分类别运动族群数据以补齐长时序 humanoid 跟踪基准不足。
  - 证明单一几何指标会漏检关键失败模式。
- 关键实验或结果：在代表性 tracking 方法中，HumanScore 能显著更好预测人类偏好，在接触滑移、踩踏时机错误等情况下与传统指标发生明显分歧，暴露“看起来对”但不可行的假高分问题。
- 适合关注的原因：对于具身 AI/人形机器人，评价偏离真实执行约束会直接导致“离线分高、部署事故多”；本文提供了从人类可感知安全性反向规范算法的范式。
- 局限性或待验证点：当前结果未覆盖所有机器人形态与任务类型；评分模型是否会被域外动作风格偏置，需在真实工况中跨平台验证。
- 对后续研究/应用的启发：可将 HumanScore 思路引入抓取、导航、协作机器人，形成“几何可行 + 人类可接受”双重验证回路，减少部署前后评测偏差。
- Obsidian 快速浏览一句总结：**该文强调机器人运动评测应以“人类可解释性与稳定性”为第一原则，而非单一轨迹误差。**

## 标准化研究框架
**Research question：** 如何构建一个既能衡量 tracking 几何精度，又能对齐人类运动感知与安全偏好的评估体系？

**Literature：** 现有 humanoid tracking benchmark 主要依赖 MPJPE/姿态误差等几何指标，缺少对接触连贯性、稳定性停顿和时序偏好的统一度量；本论文对应补齐该空白。

**Theory：** 若把运动跟踪视为“可观察状态序列映射”问题，仅最小化轨迹误差不足以保证任务执行合理性；应引入人类偏好函数作为额外约束，构成多目标评价理论。

**Hypotheses：**  
- H1：HumanScore 与人工偏好相关性高于传统 kinematic 指标。  
- H2：基准规模与动作分类多样性越高，评测对模型泛化能力和真实部署风险的识别能力越强。  
- H3：以接触稳定性为核心约束时，部分高 kinematic 分数模型会下降，反映出“虚假高分”现象。

**Method：** 通过 153 小时轨迹采集建立 12K 人类偏好对比样本；在多个追踪模型上比较 kinematic 与 HumanScore；报告失败模式归因与偏差类型。

**Data and Analysis：** 多个 motion family 作为条件切片；人类评价对形成 HumanScore 训练与验证；对比统计误差与偏好偏差之间的一致性/不一致性分布。

**Findings：** HumanScore 在关键任务失效点（接触漂移、稳定性破坏）更敏感，能够捕捉传统指标未覆盖的错误；结果支持在具身系统中引入人类感知指标。

**Conclusion：** 该论文为 embodied 跟踪任务提出了“几何 + 人类可接受性”并行评估路径，强调未来 benchmark 不能只测准度，还要测可执行性。
