# 2026-06-06 AI 论文分享

今天推荐 5 篇，重点放在 agent 系统、multi-agent 推理、安全对齐、科研协作与具身/VLM 安全。整体脉络很清楚：agent 不再只是 prompt workflow，而是在走向运行时、通信协议、上下文治理和安全边界这些更工程化的问题。

## 推荐顺序

1. [Streaming Communication in Multi-Agent Reasoning](./01-Streaming%20Communication%20in%20Multi-Agent%20Reasoning.md)
   - Spotlight：StreamMA 把 multi-agent 推理从“等上游完整输出后再传递”改成“逐步流式传递”，同时降低延迟并提升准确率。最值得看的是它提出了 step-level scaling law，把 agent 系统的扩展维度从“agent 数量”拓展到“每个 agent 的推理步数与传递时机”。
   - 链接：https://arxiv.org/abs/2606.05158

2. [Learning Agent-Compatible Context Management for Long-Horizon Tasks](./02-Learning%20Agent-Compatible%20Context%20Management.md)
   - Spotlight：AdaCoM 把上下文管理从固定摘要/截断策略变成一个外部可训练的 context manager，服务于冻结的 agent。它很适合关注 deep research、web search 和长任务 agent 的人。
   - 链接：https://arxiv.org/abs/2605.30785

3. [A Policy-Driven Runtime Layer for Agentic LLM Serving](./03-A%20Policy-Driven%20Runtime%20Layer%20for%20Agentic%20LLM%20Serving.md)
   - Spotlight：这篇从 serving stack 角度提出 agent runtime layer，试图把 prefix caching、batch shaping、fairness、tool memoization 和 safety enforcement 统一放到框架与推理引擎之间。它的价值在于把 agent 工程问题抽象成可插拔的运行时策略层。
   - 链接：https://arxiv.org/abs/2605.27744

4. [AI Agents Enable Adaptive Computer Worms](./04-AI%20Agents%20Enable%20Adaptive%20Computer%20Worms.md)
   - Spotlight：这是一篇必须谨慎阅读的安全论文。核心不是“又一个恶意软件 demo”，而是指出 open-weight LLM 加 agent 行为会改变攻击经济学，传统的中心化模型安全控制无法覆盖这种自持式威胁。
   - 链接：https://arxiv.org/abs/2606.03811

5. [Jailbreaking Vision-Language Models Through the Visual Modality](./05-Jailbreaking%20Vision-Language%20Models%20Through%20the%20Visual%20Modality.md)
   - Spotlight：VLM 安全不能只继承文本 LLM 的 safety training。这篇 ICML 2026 论文把视觉通道作为一等攻击面来分析，说明跨模态安全对齐仍有明显缺口。
   - 链接：https://arxiv.org/abs/2605.00583

## 今日观察

- Agent 系统研究正在从“能力展示”转向“运行时结构”：上下文如何删、步骤何时传、缓存如何做、策略在哪里执行。
- Safety 研究也在系统化：从文本拒答扩大到视觉输入、工具调用、运行时权限和自主传播风险。
- 对 Obsidian 后续阅读来说，可以把今天的笔记归成三个标签簇：`#AgentRuntime`、`#AgentSafety`、`#VLM安全`。
