# 2026-06-06 AI 论文分享

今天整理 5 篇近期值得分享的 AI 论文，覆盖 multi-agent reasoning、长程 agent 上下文管理、多模态视频安全、具身智能模块化设计，以及 AI4Science 里的 autonomous discovery。排序优先考虑最近 7-14 天内的发布或版本更新、选题的重要性、技术新意和阅读价值。

## 推荐顺序

1. [01-StreamMA.md](./01-StreamMA.md)
   - 论文：Streaming Communication in Multi-Agent Reasoning
   - Spotlight：这篇最值得先看，因为它把 agent 系统里常被忽略的“通信时机”做成了核心变量，直接同时打到延迟、成本和错误传播三个痛点。
   - 链接：https://arxiv.org/abs/2606.05158

2. [02-AdaCoM.md](./02-AdaCoM.md)
   - 论文：Learning Agent-Compatible Context Management for Long-Horizon Tasks
   - Spotlight：AdaCoM 把上下文管理从手工工程经验升级成可训练、可迁移的 runtime 组件，非常适合关注 deep research 和长任务 agent 的读者。
   - 链接：https://arxiv.org/abs/2605.30785

3. [03-ConceptGuard.md](./03-ConceptGuard.md)
   - 论文：ConceptGuard: Proactive Safety in Text-and-Image-to-Video Generation through Multimodal Risk Detection
   - Spotlight：它把多模态视频生成的安全防线前移到生成前和生成早期，强调图文组合风险而不是只做文本过滤。
   - 链接：https://openreview.net/forum?id=27W8fxyebT

4. [04-MOSAIC.md](./04-MOSAIC.md)
   - 论文：MOSAIC: The Right Modules for Each Task in Embodied Agents
   - Spotlight：MOSAIC 不再追求“一个大模型包打天下”，而是按任务动态拼装模块，代表了具身智能更务实的系统路线。
   - 链接：https://openreview.net/forum?id=pF9wISLUYo

5. [05-CosmoEvolve.md](./05-CosmoEvolve.md)
   - 论文：Beyond AI as Assistants: Toward Autonomous Discovery in Cosmology
   - Spotlight：这篇短论文把 AI scientist 拆成“量化目标优化”和“开放式科研协作”两类系统问题，是今天最值得留作方向性思考的一篇。
   - 链接：https://arxiv.org/abs/2605.14791

## 今日观察

- Agent 研究正在从 prompt/workflow 层，继续下沉到 runtime 层：通信协议、上下文治理、模块编排都开始成为一等问题。
- 安全边界也在变化：从文本 LLM 的拒答，扩展到多模态生成中的组合风险与前置式 guardrail。
- AI4Science 的重点正在从“模型辅助科研”转向“系统化的研究代理”，但评价标准和人机分工还远未稳定。
