# 2026-08-11 AI 论文分享

> 今日聚焦“LLM 参数高效适配、交互 Agent 修复工程化、跨形态具身导航、反射视频生成 CV 工程化评测、AI4S 医疗时序建模”。所有论文均在 2026-07-31 到 2026-08-07 之间发布（近两周），重点覆盖 LLM / Agent / CV / 具身 AI / AI4S。

## 推荐顺序

1. **[TEXAS: Task-Expert-Aware Supervision for Downstream Mixture-of-Experts LLM Adaptation](./texas-task-expert-aware-supervision.md)**
   **Spotlight：** 面向 MoE 下游适配，TEXAS 用成功/失败差异定义专家监督信号，减少无效更新并提升适配效果。
   [论文](https://arxiv.org/abs/2608.06396) · [PDF](https://arxiv.org/pdf/2608.06396)

2. **[ADIAS: Automated Design of Interactive Agentic Systems](./adias-automated-design-agentic-systems.md)**
   **Spotlight：** ADIAS 用 issue-centric 持久状态替代 candidate-centric 回放，重构 agent 自动设计的修复闭环。
   [论文](https://arxiv.org/abs/2608.06410) · [PDF](https://arxiv.org/pdf/2608.06410)

3. **[CrossTracer: Cross-Embodiment Navigation via VLA Model Reasoning and Trace Residuals Adapting](./crosstracer-cross-embodiment-navigation-vla.md)**
   **Spotlight：** CrossTracer 用统一像素轨迹先验和形态适配残差，在轮式/腿式机器人上实现更稳的跨形态导航执行。
   [论文](https://arxiv.org/abs/2608.06688) · [PDF](https://arxiv.org/pdf/2608.06688)

4. **[MirrorWorld: Taming Video Diffusion Models for Mirror Reflection Generation](./mirrorworld-video-diffusion-mirror-reflection-generation.md)**
   **Spotlight：** MirrorWorld 以语义关系蒸馏 + 几何对齐修复视频反射任务，提升镜面一致性并构建反射重建 benchmark。
   [论文](https://arxiv.org/abs/2608.07463) · [PDF](https://arxiv.org/pdf/2608.07463) · [项目页](https://youjunzhao.github.io/MirrorWorld/)

5. **[MiGHT-EHR: A Multi-task Graph Transformer for Heterogeneous Temporal EHR](./migth-ehr-multitask-graph-transformer.md)**
   **Spotlight：** MiGHT-EHR 用多任务异构图 Transformer 统一时序 EHR 的异构结构，兼顾临床多任务预测与可解释性。
   [论文](https://arxiv.org/abs/2608.06430) · [PDF](https://arxiv.org/pdf/2608.06430)

## 阅读建议

- 先读 ADIAS + TEXAS：对应 LLM 适配与 agent 修复的“训练/优化范式”。
- 再读 CrossTracer + MirrorWorld：分别对应具身 AI 与 CV 视频生成的可执行性与几何一致性问题。
- 最后读 MiGHT-EHR：作为 AI4S 的工程化主线，观察多任务共享表示如何提高复用率。
