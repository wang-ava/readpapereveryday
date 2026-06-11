# Reroute, Don\'t Remove: Recoverable Visual Token Routing for Vision-Language Models

VLM 常见做法是“删 token”，这篇工作指出这种不可逆策略会丢掉后续层才会变得重要的信息。Reroute 用“延后再路由”替代直接删除，让模型在关键层重新激活被抑制的信息，属于效率优化中的“可逆近似”方向。

- **论文标题**：Reroute, Don't Remove: Recoverable Visual Token Routing for Vision-Language Models
- **作者/机构**：Cheng-Yu Yang, Shao-Yuan Lo, Yu-Lun Liu；机构信息未在公开摘要页给出
- **发布日期/版本日期**：2026-06-10（UTC）
- **主题标签**：#Computer-Vision #Vision-Language-Model #Token-Pruning #Efficiency #LLM
- **论文链接**：[https://arxiv.org/abs/2606.12412](https://arxiv.org/abs/2606.12412)
- **PDF 链接**：[https://arxiv.org/pdf/2606.12412.pdf](https://arxiv.org/pdf/2606.12412.pdf)
- **项目/代码/数据链接（如可得）**：[https://github.com/elmma/mllm-reroute/](https://github.com/elmma/mllm-reroute/)
- **核心问题**：纯粹的 visual token pruning 在多层解码中会不可逆地删除潜在重要 token，导致 grounding 与精度波动，且难以兼顾效率与完整性。
- **方法概要**：Reroute 并非再加一个大模型层，而是一个训练自由（training-free）的 plug-in：
  1. 各路由阶段不直接删除低分 token；
  2. 被“退场”的 token 仅暂时旁路；
  3. 下一阶段重新进入候选池，被重新评分后可再次参与计算；
  4. 保持原有 attention 规则和分层 schedule 的兼容。
- **主要贡献**：
  1. 将 token 处理从一次性剪枝改为可恢复路由；
  2. 证明了路由策略可在不改变复杂度阶的前提下保留模型表现；
  3. 提供可复现实验和开源实现。
- **关键实验或结果**：在 LLaVA-1.5 与 Qwen 系列上，结合 FastV 与 PDrop 场景时，在 aggressive token reduction 条件下 grounding 性能提升，同时整体 VQA 表现保持稳定。
- **适合关注的原因**：
  1. 直接解决 VLM inference 的算力瓶颈；
  2. 技术与现有模型、路由策略兼容；
  3. 工程上易于开箱试验。
- **局限性或待验证点**：
  1. 与其他视觉任务（如高分辨率生成）下的鲁棒性还需更多验收；
  2. 路由阈值/调度策略是否跨模型稳定需再验证；
  3. 缺少更完整的端到端吞吐和能耗基准。
- **对后续研究/应用的启发**：可推动 token-level 缓解策略从“硬删”转为“软路由”，与硬件部署和长上下文 vision pipeline 结合有潜力。
- **Obsidian 快速浏览一句总结**：把 VLM 的视觉 token 剪枝从一次性丢弃改为可恢复路由，在精度与效率之间给了更好的平衡点。

## 标准化研究框架
- **Research question：** 在资源受限条件下，是否能在不改模型参数的前提下，通过可恢复 token 路由改善 VLM 的 grounding 与整体性能？
- **Literature：** 对齐视觉 token pruning 与 adaptive inference 文献，区别在于引入了可逆路由思想。
- **Theory：** 该方法建立在“token 重要性随层变化”的经验规律上，强调多阶段候选集管理比一次性过滤更贴近决策动态。
- **Hypotheses：** 可恢复路由能够减少误删关键 token，并在不显著增加推理复杂度的前提下提升下游表现。
- **Method：** 在多个 VLM backbone 上对比 baseline 剪枝策略，引入 reroute 机制并评估 grounding 与 VQA 等指标。
- **Data and Analysis：** 采用 FastV、PDrop、Nüwa 及 LLaVA-1.5/Qwen 相关基准，对 token 减少比例与性能的权衡进行定量对比。
- **Findings：** 在关键场景下，Reroute 明显优于固定删除策略；尤其在 aggressive pruning 下 grounding 提升更明显。
- **Conclusion：** 可恢复 token 路由是实用且可推广的推理优化方向，但建议继续扩展到更多视觉任务和部署条件。
