# Scaling Mixture-of-Experts Video Pretraining for Embodied Intelligence

LingBot-Video 将视频生成技术迁移到具身智能场景，关注点不在“画面更好看”，而在让模型同时学会物理可行、动作相关和任务完成导向。该工作有直接工程落地价值，因为它公开方向上明确对接 robot foundation model。

- **论文标题：** Scaling Mixture-of-Experts Video Pretraining for Embodied Intelligence
- **作者/机构：** Shuailei Ma, Jiaqi Liao, Xinyang Wang, Jingjing Wang, Chaoran Feng, Zijing Hu, Chong Bao, Zichen Xi, Yuqi Gan, Weisen Wang, Yanhong Zeng, Qin Zhao, Zifan Shi, Wei Wu, Hao Ouyang, Qiuyu Wang, Shangzhan Zhang, Jiahao Shao, Yipengjing Sun, Liangxiao Hu, Lunke Pan, Nan Xue, Kecheng Zheng, Yinghao Xu, Xing Zhu, Yujun Shen, Ka Leong Cheng；摘要中机构未细化为统一字段
- **发布日期（版本日期）：** 2026-07-08（v1）
- **主题标签：** #Embodied #CV #MoE #Video Foundation Model #Robot
- **论文链接：** https://arxiv.org/abs/2607.07675v1
- **PDF 链接：** https://arxiv.org/pdf/2607.07675v1
- **项目/代码/数据链接：**
  - Project page: https://technology.robbyant.com/lingbot-video
  - GitHub（作者生态相关）：https://github.com/robbyant/lingbot-video
  - Hugging Face Space（演示相关）：https://huggingface.co/spaces/victor/lingbot-video

## 核心问题

如何让视频基础模型兼顾视觉生成质量与动作执行可用性，减少生成器与机器人世界之间的“语义-动力学错配”。

## 方法概要

- 架构上采用 Mixture-of-Experts（MoE）替代密集模型，兼顾容量与推理效率。
- 数据上构建 profiling engine，新增大量机器人相关动作视频（操作、导航、ego 视角）。
- 训练目标中引入多维 reward：不仅优化美观和 prompt 对齐，还显式约束物理合理性与任务完成度。
- 将模型定位为动作条件世界模型，服务于 embodied policy pretraining。

## 主要贡献

1. 首次提出面向具身智能的 large-scale MoE 视频预训练路线（LingBot-Video）。
2. 强调任务-动作数据分布的重要性，缓解“通用视频模型偏好创意图像”的偏差。
3. 显式把评估标准扩展到物理合理性与可控动作执行。

## 关键实验或结果

论文强调在性能与效率上均获得综合提升，并作为社区首个开源 MoE 视频 foundation model 之一开放；摘要里未给出全部公开指标细表，但其构建与发布方向已清晰指向具身任务。

## 适合关注的原因

它将视频基础模型从“内容创作工具”推向“控制系统前置模型”，对机器人、仿真、跨实体控制策略都具备直接迁移价值。

## 局限性或待验证点

1. 公开摘要缺少完整 benchmark 表，需关注后续版本的消融与统计显著性。
2. 对不同机器人形态和动作空间的泛化仍需更多跨平台验证。
3. 推理质量与安全性（如碰撞预测）在极端场景下的边界未充分阐明。

## 对后续研究/应用的启发

- 可作为 embodied world model 与 VLA 管线的前置模块，减少对传统行为克隆数据的依赖。
- MoE 结构和多维 reward 的组合可复用到工业级 robot foundation model 的 pretraining cost-control 方案。

一句中文总结：这项工作把视频模型与 robot control 的目标对齐，代表“图像生成范式”向“可执行世界模型”迁移的重要一步。

## 标准化研究框架

- **Research question：** 视频基础模型如何在保持生成能力的同时服务真实具身任务的物理一致性与效率要求？
- **Literature：** 继承以往 video generative pretraining 与 robot world model 的桥接研究，并针对其“视觉偏好化”问题提出替代路径。
- **Theory：** 认为 MoE 与任务感知 reward 可将学习重点从“看起来好”转向“可执行动作约束更好”。
- **Hypotheses：** 机器人数据增强与多维 reward 会提高模型在控制相关任务中的有效性与效率。
- **Method：** 使用 MoE 视频骨干 + 机器人数据 profiling + 多目标 reward 微调；同时报告开源预训练权重与基础评测。
- **Data and Analysis：** 构建 robot-centric 视频混合数据，并用 video generation 与行动执行相关指标进行验证；可再通过公开 benchmark 比较效率与性能。
- **Findings：** 报告显示该路线达到预期的性能/效率平衡，且推动了面向 embodiment 的开源生态。
- **Conclusion：** 这不是传统社会科学研究；字段可解释为“模型结构与训练目标设计是否同时满足生成质量与控制可用性”的工程检验框架。
