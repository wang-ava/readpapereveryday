---
spotlight: "PACT 强调‘证据可追溯且可计数’，把重复但同源的高一致性与独立证据区分开，降低人机协作决策风险。"
---

# Not All Agreement Counts as Corroboration: Provenance-Conserving Multi-View Fusion for Typed Action Admission in Human-Robot Collaboration

## 基本信息
- **论文标题**：Not All Agreement Counts as Corroboration: Provenance-Conserving Multi-View Fusion for Typed Action Admission in Human-Robot Collaboration
- **作者**：Zekai Jin, Hanrong Zhang, Yihong Tang, Fei Hu, Zhen Dong, Yi Shao
- **机构**：未在 arXiv 元数据首屏给出
- **发布日期 / 版本日期**：2026-08-31（v1）
- **主题标签**：`具身智能` `人机协作` `多视图融合` `证据证成` `决策安全`
- **论文链接**：https://arxiv.org/abs/2609.01662v1
- **PDF 链接**：https://arxiv.org/pdf/2609.01662v1
- **项目/代码/数据链接**：https://github.com/ZekaiJ/PACT（代码与支持材料）

## 核心问题
在 embodied 系统中，不同视角重复给出同一结论时，不一定意味着“独立证据增加”。如何避免把“重复同源信号”误当作更高置信的依据？

## 方法概要
- 提出 PACT（Provenance-Conserving Typed Action Admission）机制。
- 将证据拆解为“可计数单元”，并显式建模来源关系（provenance partition）。
- 在同一来源内保留坐标一致支持、跨来源才进行聚合，防止同源放大。
- 给每个动作类型定义 admission 规则：hold / confirm / fallback。
- 在理论上证明坐标逐项交并支持下的最大学习界条件，给出单调性与稳定性性质。

## 主要贡献
1. 形式化了“agreement vs corroboration”的区别，并定义来源守恒的融合准则。
2. 提出可量化的 ncsAURC 风险覆盖指标用于多视图融合评估。
3. 在真实离线实验中展示较高通过率与低错误 admission 的平衡效果。

## 关键实验或结果
- 在 31,200 次评估、48 个场景簇中，PACT 达到 common-support normalized risk-coverage area（ncsAURC）0.0861。
- 去除构造型对照组后，相较 singleton 融合，来源分区融合使 ncsAURC 降低 0.0557，且消除了多数伪 corroboration 假象。
- 在 60 个真实离线人机协作 episode 中，camera-grouped PACT 在 Qwen3-VL-32B 设置下通过 47/57 个参考一致候选，且未观测参考不一致入场。

## 适合关注的原因
这个问题直接影响人机协作系统的安全底线：高置信误采纳常来源于“同一错误证据反复出现”。PACT 提供了处理证据来源的实用算子，非常适合安全关键场景。

## 局限性或待验证点
- 该框架依赖于可定义且可靠的 provenance partition，实践中对传感器标注/数据源管理要求更高。
- 结果集中在特定协作设置，跨任务泛化仍需更多 benchmark 佐证。
- ncsAURC 等指标是否与真实操作成本最相关还需进一步解释。

## 对后续研究/应用的启发
- 可扩展到多模态感知、自动驾驶、医疗辅助等“同源冗余误导”的场景。
- 与主动学习/不确定性估计结合可实现“按来源预算”控制决策风险。
- 为决策可解释性提供了可计算的证据流路径，便于审计与合规。

## 一句话中文速览总结
PACT 告诉我们：只有来自独立来源的重复一致才算强证据，来源追踪是 embodied 决策安全的关键。

## 标准化研究框架
- **Research question：** 在人机协作决策中，如何区分高一致性但非独立证据与可增强置信的真独立证据？
- **Literature：** 传统多视图融合多以置信度聚合为主，较少显式约束来源可分离性；本研究把 provenance 引入动作许可规则。
- **Theory：** 使用来源可计数模型定义支持运算，在单源不放大和跨源可叠加之间形成安全约束的融合规则。
- **Hypotheses：**（1）来源守恒规则能压低误采纳率（2）在复杂场景下提升 ncsAURC 指标（3）不会引入过度保守导致系统瘫痪。
- **Method：** 设计 PACT 融合规则与 admission 映射，并在构建的场景簇与离线 HRC 实验中进行对照测试。
- **Data and Analysis：** 使用 31,200 次评估与 48 个场景簇，比较 singleton、协作分区以及后验指标映射下的 ncsAURC 与通过率。
- **Findings：** 来源分区融合显著提升风险覆盖表现；高一致但低独立度的错误信号被有效抑制。
- **Conclusion：** 对安全关键 embodied 系统而言，融合策略应把“证据来源”作为第一类约束，避免 agreement 的伪强化效应。
