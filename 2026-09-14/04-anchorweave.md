# AnchorWeave: World-Consistent Video Generation with Retrieved Local Spatial Memories

**Spotlight：** 当下视频生成在长时空一致性上仍很脆，AnchorWeave 把“全局 3D 重建”改成“多局部记忆检索+融合”，是一个很实用的工程方向。

- **论文标题：** AnchorWeave: World-Consistent Video Generation with Retrieved Local Spatial Memories
- **作者/机构：** Zun Wang、Han Lin、Jaehong Yoon、Jaemin Cho、Yue Zhang、Mohit Bansal（论文页面未按统一格式列出机构）
- **发布日期 / 版本日期：** 2026-09-04（arXiv 在线版本）
- **主题标签：** `#CV` `#视频生成` `#世界一致性` `#世界模型`
- **论文链接：** [https://arxiv.org/abs/2602.14941](https://arxiv.org/abs/2602.14941)
- **PDF 链接：** [https://arxiv.org/pdf/2602.14941](https://arxiv.org/pdf/2602.14941)
- **项目/代码/数据链接：** 官网项目页：[https://zunwang1.github.io/AnchorWeave](https://zunwang1.github.io/AnchorWeave)（论文页未直接提供标准代码仓库与数据下载入口）

## 核心问题
长程相机条件下的视频生成常因全局重建误差累积，导致不同视角之间几何位置漂移。如何减少重建误差对后续帧条件注入的污染？

## 方法概要
- 用局部几何记忆替代单一全局 3D 记忆图。
- 通过 coverage-driven 检索机制选取与当前视角轨迹最相关的局部 anchor。
- 在生成过程中通过多 anchor weaving controller 融合多处几何记忆，形成跨视角对齐。

## 主要贡献
- 明确指出“单一全局 3D 重建”在长序列下的误差累积问题。
- 提出局部记忆-局部对齐机制，兼顾几何一致性与可控生成。
- 用 ablation 和分析实验拆解局部记忆、覆盖策略与多锚点控制器的作用。

## 关键实验或结果
- 报道在视频长时一致性与视觉质量上均优于基线。
- 消融显示：局部几何条件、跨视角融合和覆盖驱动检索是主要收益来源。

## 适合关注的原因
- 对做场景连贯生成、数字孪生或仿真预渲染的团队，这类局部记忆机制直接降低了场景漂移风险。
- 其思路也可迁移到闭环世界模型和交互式生成系统。

## 局限性或待验证点
- 缺少在超复杂动态场景和大量真实相机抖动条件下的规模化报告。
- 局部记忆检索成本在超长视频上可能上升，需要工程优化。
- 论文未公开全面代码和数据组织细节，复现门槛偏高。

## 对后续研究/应用的启发
可把“local memory weaving”引入 VLM 影像-动作联动任务：先保证局部几何连续，再把全局语义约束交给上层策略。

## Obsidian 快速浏览中文总结
它把长时视频世界一致性的难点拆成“局部几何记忆可控化”，在工程上比追求完整全局重建更稳妥。

## 标准化研究框架
- **Research question：** 在 camera-control 视频生成中，局部几何记忆能否抑制全局重建误差并改善长期空间一致性？
- **Literature：** 常见方法依赖全局三维重建后再条件化生成，误差会跨视角叠加；该文提出局部记忆替代方案。
- **Theory：** 通过在局部窗口检索高置信几何块并加权融合，可减少不一致几何传播，提高跨帧空间对齐。
- **Hypotheses：** H1：局部记忆优于单一全局记忆；H2：覆盖驱动检索提升关键区域一致性；H3：多锚点融合提高时间连续性。
- **Method：** 使用局部几何记忆库检索模块、multi-anchor controller 与可控生成器联合训练；对比基线方法与多个消融版本。
- **Data and Analysis：** 通过长序列空间一致性与画面质量指标，结合 ablation 分析贡献来源。
- **Findings：** 实验显示局部记忆策略明显改善一致性，且 ablation 支持关键模块有效性。
- **Conclusion：** 分布式局部记忆在生成式视频世界建模中是比“全局硬重建”更鲁棒的工程方向。
