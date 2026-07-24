# ATSplat: Compact Feed-forward 3D Gaussian Splatting with Adaptive Token Expansion

Spotlight：ATSplat 在 feed-forward 3DGS 管线中重新引入自适应场景分配思想，用 3D token 代替纯像素对齐策略，直接解决了参数冗余与建模效率之间的天然冲突。适合关注轻量重建、实时渲染与 3D 场景部署的方向。

- 论文标题：ATSplat: Compact Feed-forward 3D Gaussian Splatting with Adaptive Token Expansion
- 作者：Cho In, Jeonghwan Cho, Mijin Yoo, Gim Hee Lee, Seon Joo Kim
- 机构（如可得）：未在 arXiv 页面直接显示完整机构列表
- 发布日期或版本日期：2026-07-22（v1）
- 主题标签：#CV #3DGS #FeedforwardNeRF #NeuralRendering #TokenEfficiency
- 论文链接：https://arxiv.org/abs/2607.20417v1
- PDF 链接：https://arxiv.org/pdf/2607.20417v1
- 项目/代码/数据链接（如可得）：
  - 论文页面（含引用元信息）：https://huggingface.co/papers/2607.20417
  - 代码/模型未在摘要中给出公开链接

## 核心问题
- 传统 feed-forward 3DGS 往往沿像素回归高斯参数，导致高斯数量依赖输入分辨率和视角。
- 在复杂场景中会出现无关区域冗余建模、参数膨胀和效率损失。

## 方法概要
- 提出 **Adaptive 3D Tokens**：先从 patch-level 深度与相机线索构建稀疏 3D anchor token scaffold。
- 每个 token 回归为局部 Gaussians，并通过 learnable 3D offset 从图像网格解耦。
- 用 **Adaptive Token Expansion** 模块预测 token 不确定性，并对高不确定 token 进行可学习扩展。
- 渲染误差引导的扩展策略使模型在关键区域增加分辨能力，在稳定区域保持稀疏。

## 主要贡献
- 提出将 3DGS 的场景自适应能力显式迁移到单次前向推断范式的 token 化框架。
- 用稀疏 anchor + 可扩展 token 机制降低冗余建模。
- 保持重建质量的同时显著压缩高斯规模。
- 对真实时延与吞吐有明显优势（文中量化了 reconstruction 时延和 fps）。

## 关键实验或结果
- 在 RealEstate10K 与 DL3DV 上达到 SOTA 渲染质量。
- 与密集 feed-forward 3DGS 方法相比，Gaussians 数量降低超过 **5.7×**。
- 12 张 `512×960` 输入图像情况下，重建耗时 <1 秒（单卡商用 GPU）。
- 在同分辨率下可达 **1136 FPS** 的渲染速度（使用约 311K Gaussians）。

## 适合关注的原因
- 对需要在线或近实时场景重建的团队（机器人、数字孪生、AR）有直接工程价值。
- 体现了“可学习稀疏化 + adaptive 扩展”的实用路线，易与现有管线结合。
- 对比传统逐像素回归，方法更契合边缘设备和高吞吐场景。

## 局限性或待验证点
- 摘要中未给出更大规模跨场景泛化与极端照明、纹理稀缺场景结果。
- 未见代码与训练/评估细节完整公开，外部复现实验门槛较高。
- 实时指标主要来自公开数据集基准，真实工业数据需进一步验证。

## 对后续研究/应用的启发
- 可作为高效 3DGS 前端，减少在高分辨率视频场景中的算力占用。
- token 级不确定性驱动可扩展思路可迁移到视频、NeRF 变体和体素压缩任务。

## 一句 Obsidian 快速浏览总结
一句话：ATSplat 的核心贡献是把 3DGS 从“输入网格驱动”改为“场景复杂度驱动”的 token 重构，提高了速度与压缩率。

## 标准化研究框架
- **Research question：** feed-forward 3D 场景重建能否在保持质量的前提下，通过可学习 token 稀疏化显著降低高斯冗余？
- **Literature：** 与经典 3DGS、NeRF 系列和快速前向重建工作衔接，尤其关注输入分辨率依赖性的降低。
- **Theory：** 引入可展开 token 层级实现参数复杂度与场景复杂度的耦合调节。
- **Hypotheses：** token 稀疏 scaffold + 不确定性扩展能在复杂区域集中 capacity，在规则区域减少无效高斯。
- **Method：** 构建 3D anchor token、局部高斯回归、uncertainty 预测与分层扩展，并在统一训练目标下联合优化。
- **Data and Analysis：** 在 RealEstate10K、DL3DV 进行重建质量与速度-容量指标评估，并比较 Gaussians 数量、fps 与重建时延。
- **Findings：** 论文摘要显示方法在质量和效率上同时提升，且模型规模更轻量。
- **Conclusion：** 本文验证了 token 化前向重建框架在 3DGS 的有效性，支持后续在移动端与实时应用落地。
