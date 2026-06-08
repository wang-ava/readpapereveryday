# 2026-06-08 AI 论文分享

今天整理 5 篇近期值得分享的 AI 论文，覆盖视频多模态理解、theory-building world models、具身数据生成、multi-agent deliberation 与 AI4Science。排序优先考虑最近 7-14 天内发布或更新、议题的重要性、技术新意、来源可信度与实际阅读价值。

## 推荐顺序

1. [01-VSTAT.md](./01-VSTAT.md)
   - 论文：Benchmarking Visual State Tracking in Multimodal Video Understanding
   - Spotlight：它非常直接地点破了一个常被高分 benchmark 掩盖的问题: 现在的视频 MLLM 可能会“说推理”，但并不会稳定地“跟踪状态”。
   - 链接：https://arxiv.org/abs/2606.03920

2. [02-Learning-to-Theorize.md](./02-Learning-to-Theorize.md)
   - 论文：Learning to Theorize the World from Observation
   - Spotlight：这篇不是在堆更大的 world model，而是在问“理解世界”是否应该意味着能形成可组合的解释性 theory，这个问题本身就很值得看。
   - 链接：https://arxiv.org/abs/2605.03413

3. [03-Scene2Demo.md](./03-Scene2Demo.md)
   - 论文：Scene2Demo: Self-Evolving Embodied Data Generation via Object-Action Graph
   - Spotlight：它把“从一张真实图生成可执行机器人数据”的链条打通了，价值在于为 embodied learning 提供更自动化的数据工厂思路。
   - 链接：https://openreview.net/forum?id=88IawleLNi

4. [04-Agent-MoE.md](./04-Agent-MoE.md)
   - 论文：Multi-Agent Systems are Mixtures of Experts: Who Becomes an Influencer?
   - Spotlight：这篇值得看，因为它不再只比较“多 agent 比单 agent 强不强”，而是试图解释 agent 间影响力到底如何形成。
   - 链接：https://arxiv.org/abs/2605.25929

5. [05-Spectra-as-Language.md](./05-Spectra-as-Language.md)
   - 论文：Spectra as Language: Large Language Models for Scalable Stellar Parameter and Abundance Inference
   - Spotlight：它把光谱当作序列来建模，是 LLM 范式向科学测量数据迁移的一个很干净、也很有启发性的 AI4Science 样本。
   - 链接：https://arxiv.org/abs/2605.22162

## 今日观察

- 视频理解方向正在从“能否答对问题”转向“能否持续追踪随时间变化的状态”，这会更真实地暴露多模态模型的感知短板。
- world model 与 embodied AI 都在明显走向“结构化中间表示”，无论是 theory、program、object-action graph 还是可量化的 influence / competence。
- agent 研究开始从纯工程技巧进入更可解释的分析框架，说明下一阶段竞争点会落在 orchestration 原理，而不只是 prompt 手法。
- AI4Science 的一条稳健路线不是追求通用智能叙事，而是把 LLM 当成高维科学序列的 scalable representation learner。
