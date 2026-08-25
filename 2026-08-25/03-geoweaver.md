# GeoWeaver: Accurate Long-Sequence 3D Reconstruction via Hierarchical Geometric Assembly

GeoWeaver 关注长序列 3D 重建中“长序列漂移”难题：单段预测虽快，但跨段拼接会带来尺度与姿态累积误差。本文给出一套几何先验+测试时适配的统一框架，既保留局部精度又修复全局一致性。

它的实用性在于可以兼容不同几何先验模型做后处理，不依赖单一 backbone 重训练，适合直接接入现有长序列重建流水线。

## 论文标题
GeoWeaver: Accurate Long-Sequence 3D Reconstruction via Hierarchical Geometric Assembly

## 作者/机构
- 作者：Tinghao Jiang, Sheng Tang, Shengzhe Wei, Juntong Fang, Weiqi Zhang, Junsheng Zhou, Zesong Li
- 机构：arXiv 页面未公开机构信息

## 发布日期/版本日期
- 版本发布日期：2026-08-18（v1，`2026-08-18T05:29:31Z`，对应 Asia/Shanghai 2026-08-18）

## 主题标签
#CV #3DReconstruction #SfM #GeometricConsistency #TestTimeAdaptation

## 论文链接
- https://arxiv.org/abs/2608.17389v1

## PDF 链接
- https://arxiv.org/pdf/2608.17389v1

## 项目/代码/数据链接
- 项目页：https://kosmoresearch.github.io/GeoWeaver/
- 代码：项目页待确认（未在 arXiv comment 中给出仓库链接）
- 数据：公开基准按文内描述，需在实验页确认

## 核心问题
长视频序列难以直接做全局联合优化：分块推理降低了显存压力，但会引入尺度漂移与跨段对齐误差。如何在保持分块效率的前提下，恢复全局几何一致性？

## 方法概要
- 构建 Geometric Prior Model (GPM)，输出 chunk 级深度、置信度与相机参数作为可调先验。
- 测试时引入层级适配（TTA）：
  1) 顺序初始化
  2) 全局 chunk-level Sim(3) 对齐
  3) 深化的相机姿态、深度尺度与内参联合优化
- 引入密集对应约束：相邻、跨块、长程约束。
- 优化目标联合 2D 重投影与 3D 一致性残差，采用鲁棒 CDF 风格损失。

## 主要贡献
1. 将 GPM 与 TTA 分离设计，解决“局部预测快、全局漂移”悖论。
2. 提供分层的几何装配策略，能兼容不同几何先验模型。
3. 在长序列任务上提升了相机轨迹精度与点云全局一致性。

## 关键实验或结果
- 在多类长序列基准上，GeoWeaver 在相机精度、全局一致性与点云质量方面均有提升。
- 消融实验显示每个 TTA 阶段均有贡献。
- 将同一 TTA 迁移到不同 GPM，均可明显改进其轨迹估计，验证方法非特定模型耦合。

## 适合关注的原因
相机轨迹与尺度是长序列重建的核心稳定性瓶颈；GeoWeaver 的“先局部推理、后全局校正”思路对工程落地友好，尤其适用于需要大规模室外/室内扫描的应用。

## 局限性或待验证点
- 论文摘要未提供完整参数量和复杂度分析，难以直接估算部署成本。
- 对极端动态场景与强光照突变条件的鲁棒性未在摘要中展开。
- 依赖高质量跨块对应的可获得性，真实数据中会受遮挡与纹理贫乏影响。

## 对后续研究/应用的启发
- 可作为 NeRF、3DGS、SLAM 等 pipeline 的“后处理几何对齐层”复用。
- 对多模型并行方案（不同 GPM）可形成统一适配层，降低重建系统维护成本。
- 有望与在线/实时系统结合，在高帧率场景实现增量式几何修正。

## 适合 Obsidian 快速浏览的中文总结
一句话：GeoWeaver 用分块几何先验 + 阶段化测试时对齐，实现了大规模重建中的局部精度与全局一致性的协同。

## 标准化研究框架
**Research question：** 不做纯模型单点提升，而是研究“如何在长序列重建中恢复全局几何一致性”：分块先验是否能在测试时阶段被高效修复到统一尺度和姿态。

**Literature：** 常见方法要么偏向 feed-forward 准确率，要么偏向大规模联合优化，难兼顾显存与全局一致性；本工作提供一个分层修正替代方案。

**Theory：** 对应于分层优化理论：先构造高置信 chunk-level 先验，再通过全局 Sim(3) 与联合残差优化抑制漂移项。

**Hypotheses：** 如果引入分级对齐和跨块约束，局部深度先验可保留局部质量，同时显著改善长程尺度与轨迹一致性。

**Method：** 使用统一 TTA 流程处理 GPM 输出：顺序初始化 → Sim(3) 对齐 → 深度与相机参数联合细化；并通过消融隔离各阶段贡献。

**Data and Analysis：** 以公开长序列基准为测试池，比较几何精度（轨迹、点云质量）和消融曲线，分析每阶段对性能提升的边际贡献。

**Findings：** 三阶段流程对指标都有正向贡献，且方法可迁移到不同几何先验模型，增强了通用性。

**Conclusion：** GeoWeaver 提供“模型无关的几何装配层”思路，在工程化 3D 重建系统中比单纯换模型更容易落地。
