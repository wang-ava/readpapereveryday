# 2026-08-12 AI 论文分享

> 今日聚焦“自进化 MLLM、执行决策型 LLM Agent、机器人生态统一、物理世界模型与医学像素语言一体化”三线并行。所有论文均在 2026-08-10 到 2026-08-11 期间发布（近 7-14 天）。

## 推荐顺序

1. **[Perception Before Supervision: Self-Contained Visual Distillation from Counterfactual Blind Spots](./counterfactual-visual-distillation-cvpd.md)**
   **Spotlight：** 通过反事实盲点将 MLLM 视觉模型无法充分利用的关键区域变成密集监督信号，实现无需外部教师的自蒸馏。
   [论文](https://arxiv.org/abs/2608.09931) · [PDF](https://arxiv.org/pdf/2608.09931)

2. **[XPolicyLab: A Unified Standard and Open Ecosystem for Robot Policy Evaluation and Deployment](./xpolicylab-robot-policy-ecosystem.md)**
   **Spotlight：** XPolicyLab 把多策略接入多环境成本从 O(NM) 降到 O(N+M)，直接推动可复现的机器人评估生态。
   [论文](https://arxiv.org/abs/2608.09892) · [PDF](https://arxiv.org/pdf/2608.09892) · [项目主页](https://xpolicylab.github.io/) · [代码](https://github.com/XPolicyLab/XPolicyLab)

3. **[Learning How the World Evolves: Extrapolative Video World Models via Latent Dynamics Reasoning](./latent-dynamics-reasoning-video-world.md)**
   **Spotlight：** 用显式动力学积分替代纯像素拟合，显著提升视频世界模型的外推能力和推理效率。
   [论文](https://arxiv.org/abs/2608.09926) · [PDF](https://arxiv.org/pdf/2608.09926) · [项目页](https://lat-dyn-reason.github.io/)

4. **[From Relevance to Execution Utility: Reward-Aware Dynamic Execution Gating for Skill-Based LLM Agents](./radeg-agent-execution-gating.md)**
   **Spotlight：** RADEG 不是再学一次检索，而是为技能执行加一道价值闸门，实现更稳的预算控制。
   [论文](https://arxiv.org/abs/2608.09168) · [PDF](https://arxiv.org/pdf/2608.09168)

5. **[MedPixel: A Unified Pixel-Language Model for Medical Reasoning and Segmentation](./medpixel-medical-pixel-language-model.md)**
   **Spotlight：** MedPixel 通过 language-mask 一体化，把医学推理与像素级分割放在统一训练目标里。
   [论文](https://arxiv.org/abs/2608.09818) · [PDF](https://arxiv.org/pdf/2608.09818) · [代码](https://github.com/yhy-whu/Medpixel)
