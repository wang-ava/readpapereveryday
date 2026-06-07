# 2026-06-07 AI 论文分享

今天整理 4 篇近期值得分享的 AI 论文/研究成果，覆盖 AI4Science、多模态视频理解、具身智能中的主动空间认知，以及带形式化安全约束的机器人技能优化。排序优先考虑最近 7-14 天内发布或更新、议题的重要性、技术新意、可信度与实际阅读价值。

## 推荐顺序

1. [01-CoScientist.md](./01-CoScientist.md)
   - 论文：Accelerating scientific discovery with Co-Scientist
   - Spotlight：这篇最值得先看，因为它把 multi-agent system 从“做任务”推进到“做科研假设生成”，而且已经给出真实湿实验验证，不只是 demo。
   - 链接：https://www.nature.com/articles/s41586-026-10644-y

2. [02-VSTAT.md](./02-VSTAT.md)
   - 论文：Benchmarking Visual State Tracking in Multimodal Video Understanding
   - Spotlight：VSTAT 很重要，因为它指出当前视频 MLLM 不是真的“看懂了长视频”，而是卡在持续状态跟踪这条关键能力线上。
   - 链接：https://arxiv.org/abs/2606.03920

3. [03-Theory-of-Space.md](./03-Theory-of-Space.md)
   - 论文：Theory of Space: Can Foundation Models Construct Spatial Beliefs through Active Exploration?
   - Spotlight：它把 embodied agent 的“空间心智地图”单独抽出来测，清楚暴露出视觉感知、belief stability 与 belief revision 的系统性短板。
   - 链接：https://openreview.net/forum?id=c2cxLvsdUp

4. [04-VASO.md](./04-VASO.md)
   - 论文：Automated Skill Optimization via Formal Verification for Embodied Agents
   - Spotlight：VASO 代表了一条很务实的路线：不重新训练大模型，而是把自然语言 skill 变成可验证、可迭代修正的外部程序接口。
   - 链接：https://openreview.net/forum?id=TxGsSn4nrZ

## 今日观察

- “Agent” 研究继续向更高价值场景外溢：从网页操作、工具调用，进一步进入科研假设生成与实验协同。
- 多模态系统的短板越来越清楚地落在长期状态追踪、空间 belief 构建和错误修正，而不只是单帧感知或短链推理。
- 具身智能的一个明显趋势是把 runtime、skill abstraction、formal verification 这些系统层问题抬升为一等研究对象。
