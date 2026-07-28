# Gaze-DETR: Top-Down Guidance Through Priority Maps for Infrared Weak-Small UAV Detection with DETR

Spotlight：这篇 CV 工作的重点不只是“再提一个 DETR 变体”，而是把人类视觉注意机制以 priority map 的形式引入候选生成，解决红外小目标检测里目标细碎、低对比且易淹没的问题，值得关注其“任务驱动搜索”设计是否可迁移到其他检测场景。

- 论文标题：Gaze-DETR: Top-Down Guidance Through Priority Maps for Infrared Weak-Small UAV Detection with DETR
- 作者：Nian Liu, Yuxin Yang, Shubo Lin, Sikui Zhang, Liang Li, Boyu Cai, Yizheng Wang, Weiming Hu, Jin Gao
- 机构（如可得）：未在当前 arXiv 页面直接给出机构信息
- 发布日期或版本日期：2026-07-21（v1）
- 主题标签：#CV #DETR #Infrared #SmallObjectDetection #PriorityMap #Attention
- 论文链接：[https://arxiv.org/abs/2607.19040v1](https://arxiv.org/abs/2607.19040v1)
- PDF 链接：[https://arxiv.org/pdf/2607.19040](https://arxiv.org/pdf/2607.19040)
- 项目/代码/数据链接（如可得）：代码仓库：[https://github.com/nliu-25/Gaze-DETR-Top-Down-Guidance-Through-Priority-Maps-for-Infrared-Weak-Small-UAV-Detection-with-DETR](https://github.com/nliu-25/Gaze-DETR-Top-Down-Guidance-Through-Priority-Maps-for-Infrared-Weak-Small-UAV-Detection-with-DETR)

## 核心问题
- 红外小目标往往尺寸很小、能见度低、容易被噪声和背景遮挡，单框监督容易在关键细节阶段丢信号。
- 传统检测器从最终框预测回推“该优先看哪里”能力有限，导致定位前的搜索步骤缺乏可解释先验。
- 如何让检测器在定位前先形成“top-down 优先级”，让后续解码更贴合任务与视觉证据？

## 方法概要
- 提出 Gaze-DETR：先学一个 priority map，再进行目标检测。
- 设计 priority head 输出归一化空间优先图，指引模型在后续阶段关注高价值区域。
- 引入 Residual Priority-Guided Feature Modulation（RPFM）对高优先区域进行增强，保留多尺度语义。
- 提出 Priority-Guided Anchor Query Injection（PAQI），把优先区域转换为解码阶段 anchor query。
- 提供三套优先监督：box-derived map、真实 gaze map、通过 gaze-box 关系迁移得到 pseudo-gaze map；并构建 TIR-UAV120-Gaze 数据用于验证。

## 主要贡献
- 明确了“先搜索、后定位”的训练范式，将任务驱动注意机制与 DETR 解码流程融合。
- 把注意先验作为结构化输入而非后处理技巧，提升对弱目标证据的保留与检索。
- 给出了多监督策略比较，说明 pseudo-gaze 也能在缺失真实 gaze 标注时提升性能。

## 关键实验或结果
- 在 TIR-UAV120-Gaze 上，box-supervision、real-gaze supervision 下均有较高表现，文中给出 85.76 mAP50 / 88.77 F1 及 86.18 mAP50 / 89.00 F1。
- 在 Anti-UAV410 上，分别报告了 87.06 mAP50 / 90.90 F1 与 87.08 mAP50 / 90.43 F1（pseudo-gaze 较强鲁棒）。
- 与传统单纯边界框方案相比，文中论证优先图学习能在 clutter/噪声条件下提供更稳定的先验引导。

## 适合关注的原因
- 红外弱小目标是高风险安全领域（如安防、边境、航空监测）常见场景，本方法强调搜索策略可解释性，部署风险较低。
- 论文兼顾了标注成本：不仅依赖真实 gaze，还给出 pseudo-gaze 方案，工程应用更务实。
- 其“先引导后定位”的框架可迁移到小目标或目标稀疏任务，而非只适用于 UAV 这一特定场景。

## 局限性或待验证点
- 实验基线主要集中在红外目标检测场景，跨模态泛化（可见光、雷达）尚未在文中充分验证。
- pseudo-gaze 构造依赖 paired 注释学习，弱标签域可能影响迁移质量。
- 检测器仍受数据分布影响，极端恶劣天气和传感器噪声条件下的稳健性需补实验。

## 对后续研究/应用的启发
- 可尝试把 priority map 机制接入行人检测、工业缺陷检测等小目标任务，评估标注效率提升。
- 为真实部署场景可加入在线优先图校准器（curriculum/分布漂移检测），提高长期适配能力。
- 结合知识蒸馏将优先机制压缩到边缘端可部署模型，增强嵌入式可用性。

## 一句 Obsidian 快速浏览总结
一句话：这篇论文用可学习优先图解决红外小目标“先找不到再定位”的核心瓶颈，思路上可直接复用到更多稀疏检测任务。

## 标准化研究框架
- **Research question：** 先构建任务驱动优先图再进行 DETR 解码，能否稳定提升弱小红外目标的检测精度与召回边界？ 
- **Literature：** 基于 DETR 与视觉注意机制，补足了小目标任务中“前期候选引导不足”的短板。
- **Theory：** 在特征空间中显式引入空间优先先验，可提高网络在高噪声条件下的有效信号检索概率。
- **Hypotheses：** 优先图引导能提高微弱目标的检索命中率，且 pseudo-gaze 监督可在缺失真实 gaze 时保持可比性能。
- **Method：** 构建 priority head、RPFM 和 PAQI 三模块，通过三种监督信号训练，并在多个红外小目标基准比较 mAP/F1。
- **Data and Analysis：** 使用 TIR-UAV120-Gaze 与 Anti-UAV410 数据，比较不同监督策略下指标变化，定量评估召回与精度权衡。
- **Findings：** 论文报告优先图引导在不同注释条件下均有明显收益，且在 real/pseudo gaze 体系间表现接近。
- **Conclusion：** 在弱目标红外检测中，先验引导式的 top-down 检测路径可作为更稳健的替代范式。
