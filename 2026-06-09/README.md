# 2026-06-09 AI 论文分享

今天整理 4 篇近两周内值得分享的 AI 论文，主题集中在 embodied AI、video world model 与 foundation-model planning。它们虽然题目不同，但共同指向一个更基础的问题：模型不仅要“会答题”或“会生成”，还要在长时序里稳定地记住空间、更新信念，并把这些中间状态转成可靠行动。

## 推荐顺序

1. [01-Theory-of-Space.md](./01-Theory-of-Space.md)
   - 论文：Theory of Space: Benchmarking Active Spatial Belief Construction and Revision in Foundation Models for Embodied Agents
   - Spotlight：这篇最值得先看，因为它把“空间理解”从静态 perception benchmark 推进到了主动探索和 belief revision，直接暴露 agent 为什么一进真实环境就变笨。
   - 链接：https://openreview.net/forum?id=c2cxLvsdUp

2. [02-GIM-World.md](./02-GIM-World.md)
   - 论文：Geometry-Aware Implicit Memory for Video World Models
   - Spotlight：它代表了一条很强的 world model 路线：不再存更多帧，而是把跨视角几何结构压进紧凑隐式记忆里，去换长时一致性。
   - 链接：https://arxiv.org/abs/2606.02436

3. [03-MOSAIC.md](./03-MOSAIC.md)
   - 论文：MOSAIC: The Right Modules for Each Task in Embodied Agents
   - Spotlight：这篇不是继续堆一个“更大全能模型”，而是把 embodied agent 设计成按任务动态组装 module graph，这个方向很现实，也很工程化。
   - 链接：https://openreview.net/forum?id=pF9wISLUYo

4. [04-Semantic-Horizons.md](./04-Semantic-Horizons.md)
   - 论文：Semantic Horizons: Information-Theoretic Limits of Foundation Model-Guided Embodied Planning
   - Spotlight：它难得地给 embodied foundation models 的长时失败提供了理论刻画，不再只是经验上说“任务一长就掉”。
   - 链接：https://openreview.net/forum?id=CNej21yr6r

## 今日观察

- embodied AI 的瓶颈正在从单点能力转向“中间状态管理”，也就是 memory、belief、subgoal 与 replanning。
- video/world model 研究开始明显强调几何一致性，而不是只追求视觉 plausibility。
- 主动探索能力依然落后于被动问答能力，说明很多 foundation model 还没有形成稳定可更新的 spatial belief。
- 研究范式正在分化为两条路线：一条偏系统工程，强调模块组合与检索式 memory；另一条偏理论，试图给规划 horizon 和失败边界建立可解释公式。
