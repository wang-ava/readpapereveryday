# 2026-08-17 AI 论文推荐

今日共筛选 5 篇（覆盖 LLM、Agent、CV、具身智能、AI4S）：

1. **AutoDesign: Meta-Harness Optimization for Long-Horizon Agentic Design**
   - 链接：[01-autodesign-meta-harness-agentic-design.md](./01-autodesign-meta-harness-agentic-design.md)
   - Spotlight：把 LLM Agent 的长链路执行改成“可自举的元 harness 优化”，用少量反馈闭环持续改进工具策略。对需要复杂生成/排版/工程串联的自动化场景尤其有参考价值。
   - 推荐顺序：★★★★★

2. **HumanTracker: Towards Comprehensive and Human-Aligned Motion Tracking Benchmark**
   - 链接：[02-humantracker-motion-tracking-benchmark.md](./02-humantracker-motion-tracking-benchmark.md)
   - Spotlight：给 humanoid motion tracking 提供了“人类偏好对齐 + 接触约束”两层评估，可能更接近真实部署中的动作可行性标准。适合作为 embodied benchmark 反思标准化案例。
   - 推荐顺序：★★★★☆

3. **QuoteBench: How Matched Scores Can Hide Command-Path Failures**
   - 链接：[03-quotebench-command-path-failure.md](./03-quotebench-command-path-failure.md)
   - Spotlight：强调 agent scoring 要区分“生成是否正确”和“执行链路是否正确”，对 LLM coding agent 的上线评估方法有直接迁移价值。尤其适合工具调用场景的安全基线建设。
   - 推荐顺序：★★★★☆

4. **Intervention-Aware Clinical World Model for Post-Op Outcome Forecasting in Cardiology**
   - 链接：[04-intervention-aware-clinical-world-model.md](./04-intervention-aware-clinical-world-model.md)
   - Spotlight：首次把术后随访时序事件显式建模为 intervention-aware latent transition，直接提升临床预测可解释性和风险更新能力。是 AI4S 中 temporal EMR 世界模型方向的重要示例。
   - 推荐顺序：★★★★☆

5. **HounsWorld: A Multimodal World Model for Hidden Patient-State Readout, Reconstruction, and Simulation**
   - 链接：[05-hounsworld-multimodal-patient-state-model.md](./05-hounsworld-multimodal-patient-state-model.md)
   - Spotlight：提出共享隐状态视图，把 CT 读出、重建、模拟统一为同一模型任务链，兼顾诊疗报告、低剂量去噪与条件生成，贴近临床多任务协同需求。 
   - 推荐顺序：★★★★☆

## 使用说明
- 关键词建议：`LLM` `Agent` `CV` `EmbodiedAI` `AI4S`
- 当日日期目录：`2026-08-17`
- 提交口径：`Add AI paper notes for 2026-08-17`
