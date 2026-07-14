# Video Generation Models are General-Purpose Vision Learners

## Spotlight（今日速读）
论文提出反向思路：与其把 video generation 当成“只会画画”的单点能力，不如把它当作通用视觉认知的预训练范式；结果显示对多任务视觉任务同样有效。

## 论文标题
Video Generation Models are General-Purpose Vision Learners

## 作者/机构
- 作者：Letian Wang, Chuhan Zhang, Rishabh Kabra, Jasper Uijlings, Steven Waslander, Andrew Zisserman, Joao Carreira, Kaiming He, Misha Andriluka, Eduard Gabriel Bazavan, Andrei Zanfir, Cristian Sminchisescu
- 机构：arXiv 结构化元数据未直接列出完整机构；摘要页和项目页可继续补齐。

## 发布日期
2026-07-10（v1，arXiv）

## 主题标签
#CV #VLM #VideoGeneration #GeneralistModel #Pretraining #VisionPerception

## 论文链接
https://arxiv.org/abs/2607.09024

## PDF 链接
https://arxiv.org/pdf/2607.09024v1

## 项目/代码/数据链接（如可得）
- 项目页： https://genception.github.io
- 代码/数据：摘要未给出仓库与数据集下载链接，可关注项目页后续更新

## 核心问题
视觉模型长期在任务单一或多模态局部联合中训练，迁移到新任务时仍需专门微调。论文核心问题是：大规模 text-to-video 生成预训练是否能成为“更接近通用视觉智能”的核心范式？

## 方法概要
- 采用预训练的视频生成扩散主干作为视觉感知“骨架”。
- 定义 GenCeption feed-forward 形式的感知模型：使用文本指令在不同视觉任务间 steer。
- 在不改变预训练主干结构的前提下，对比 V-JEPA、Video MAE 等替代预训练范式。
- 评测覆盖深度估计、表面法线、相机姿态、语义分割、3D 关键点等任务。

## 主要贡献
- 提出从“生成任务”到“通用视觉学习任务”的方法论转换。
- 在不同下游任务上展现跨任务统一能力，降低“每个任务一套 backbone”的设计负担。
- 报告了在不同数据规模下的扩展行为，支持用更高参数效率评估预训练投资回报。

## 关键实验或结果
- 在多项视觉任务上达到 SOTA 或接近 SOTA，与 DepthAnything3、SAM3、VGGT-Omega、D4RT 等模型对比具优势。
- 与其他预训练范式（如 Video MAE）对比，在可比设置下表现更好。
- 初步发现合成数据规模下具备显著数据效率：某些设置可在较少训练数据（论文摘要中给出 7 到 500 的缩量级提升）下达到领先模型性能。
- 在未见域（合成动物/机器人视频）有一定泛化现象。

## 适合关注的原因
该工作若持续稳健，说明高质量的生成模型可能直接成为“多任务视觉基础模型”的预训练母体，对自动驾驶、AR、机器人 perception stack 与 3D 视觉系统都有潜在长期价值。

## 局限性或待验证点
- 当前报告的泛化行为主要来自论文摘要级别描述，需看完整实验确认消融完整性。
- 真实部署成本与推理延迟在通用化中可能成为新瓶颈。
- 数据来源与版权边界（尤其是长序列视频）在工程落地时需要明示。

## 对后续研究/应用的启发
- 可尝试把该范式移植到 3D 场景理解流水线，减少专用模型并行开发成本。
- 对于多任务 CV 平台，单一生成主干 + 多任务 head 可能带来更低维护成本。
- 可与 embodied 场景结合，构造视觉基底先验与真实动作策略的统一表示层。

## 一句话总结
这篇文章的重点是把“会生成”升级为“会理解”，并展示通用视频生成主干在多个视觉任务上的跨域潜力。

## 标准化研究框架
- **Research question：** 文本生成式视频模型是否能在不专门微调任务头的条件下，作为通用视觉学习 backbone 支撑多种 CV 任务？
- **Literature：** 连接生成模型与视觉基础模型两类路线；其创新点在于反转任务假设：生成范式可服务广谱感知。
- **Theory：** 非社会科学语境下可等价为“跨任务表征共享假设”：视频时空先验同时服务多任务映射。
- **Hypotheses：** H1：基于 text-to-video 主干的统一模型在多数任务上不劣于单任务特化模型；H2：不同任务可通过 prompt/头部调度实现统一推理；H3：模型对数据规模具更高效率。
- **Method：** 在统一主干下评测 depth、normal、pose、segmentation、3D keypoint 等任务，按统一数据预处理和预算上对比基线。
- **Data and Analysis：** 使用公开任务标准集与若干规模消融，分析跨任务性能与数据规模敏感性。
- **Findings：** 摘要显示本方法在若干任务达到 SOTA 或近似 SOTA；并观察到合成到真实/跨域样本一定泛化趋势。
- **Conclusion：** 视频生成范式具有成为通用视觉预训练来源的潜力，关键在于验证其跨任务稳定性与生产可用成本。
