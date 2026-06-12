# Light-WAM: Efficient World Action Models with State-Fusion Action Decoding

Light-WAM 在机器人/具身任务里用更轻量的世界动作建模链路替代重型生成式方案，优点是推理成本更低，同时保留对动态时序关系的建模能力。

- **论文标题**：Light-WAM: Efficient World Action Models with State-Fusion Action Decoding
- **作者/机构**：Ziang Li，Dongzhou Cheng，Yibin Wang，Shiyue Wang，Xiaoyang Xu，Lingxuan Weng，Juan Wang，Jiaqi Wang；机构：Wuhan University（部分提交信息显示）
- **发布日期/版本日期**：2026-06-06（arXiv:2606.08242，Submitted by on Jun 9）
- **主题标签**：#EmbodiedAI #Robotics #WorldActionModel #CV #ActionModel #Video
- **论文链接**：[https://arxiv.org/abs/2606.08242](https://arxiv.org/abs/2606.08242)
- **PDF 链接**：[https://arxiv.org/pdf/2606.08242.pdf](https://arxiv.org/pdf/2606.08242.pdf)
- **项目/代码/数据链接（如可得）**：论文页显示 GitHub 资源入口；当前自动抓取中未展开到具体仓库 URL（可在 Hugging Face 论文页继续导航）
- **核心问题**：现有 world action model 常依赖大规模生成式架构，训练与推理成本高，不利于可部署的闭环机器人策略。
- **方法概要**：
  1. 使用紧凑视频 backbone + 降采样潜空间做 future-video supervision；
  2. 动作预测阶段引入 StateFusionActionExpert；
  3. 通过 learned-query pooling 融合多层适配状态，并单步预测 action chunk；
  4. 避免昂贵的生成式动作专家。
- **主要贡献**：
  1. 在效率优先前提下保留 world-action建模能力；
  2. 引入跨层状态融合机制，降低动作预测中的时序解码负担；
  3. 实证验证了参数量压缩（0.44B）与推理效率之间的可行平衡。
- **关键实验或结果**：在 LIBERO 与 RoboTwin 2.0 上均有可用表现；推理延迟约 72.03ms，峰值显存约 4.1GiB，训练吞吐有提升。
- **适合关注的原因**：
  1. 兼顾 CV 与具身 agent 的实时性需求；
  2. 对边缘机器人或受限算力环境更友好；
  3. 兼容多任务执行链路，具备工程化潜力。
- **局限性或待验证点**：
  1. 抽象化指标丰富，但复杂真实环境域适配度未充分展开；
  2. 对多模态感知（语音/语义）融合路径不够细化；
  3. 大规模长期策略稳定性仍待更长 horizon 任务验证。
- **对后续研究/应用的启发**：可与 VLA/LLM-agent 控制栈对接，形成“视觉预测+轻量动作头”组合路线，适配多任务室内机器人。
- **Obsidian 快速浏览一句总结**：Light-WAM 用轻量化世界动作模型把“动作生成”成本降下来，同时保留时序推理能力。

## 标准化研究框架
- **Research question：** 在有限算力下，如何在保持动作质量的同时降低 world action model 的训练与推理成本？
- **Literature：** 属于世界动作模型（WAM）与机器人动作建模主线，区别在于与其依赖重型生成模型的前辈相比强调轻量化与推理效率。
- **Theory：** 通过压缩潜空间和跨层状态融合，降低动作解码复杂度；使用单步 action chunk 预测替代复杂长链生成。
- **Hypotheses：** 对于具身操控任务，轻量 WAM 与状态融合头可在成本可控下保持可用性能。
- **Method：** 训练 compact video backbone + 下采样 future-video监督 + state-fusion action head；在 LIBERO / RoboTwin 2.0 做跨任务评测。
- **Data and Analysis：** 使用标准操控基准任务数据；评估指标包含推理延迟、显存占用、吞吐量与任务成功率。
- **Findings：** 在多任务下保持可用性能，且较大模型方案有明显效率优势。
- **Conclusion：** Light-WAM 为具身智能提供了更具工程可行性的动作建模方向，但需要更大规模现实场景和多模态反馈验证。
