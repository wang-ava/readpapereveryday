# 2026-08-08 AI 论文分享

> 今日选题聚焦“模型可否真正学会筛选、修复与协同决策”：包含 LLM 上下文鲁棒性、Web Agent 评测边界、反馈式修复记忆、多人世界模型与代谢组学 AI4S 的两条高价值线索。全部论文均为 2026-08-06 发布的 arXiv 文稿。

## 推荐顺序

1. **[Learning When to Trust via Selective Context Preference Optimization](./scope-selective-trust.md)**  
   **Spotlight：** 通过 MIST 四条件与 SC2W 指标，把“抗误导”问题升级为“选择性信任”问题，降低误导翻转风险并保留有用上下文收益。
   [论文](https://arxiv.org/abs/2608.06377) · [PDF](https://arxiv.org/pdf/2608.06377) · [项目页](https://worldbench.github.io/scope/) · [代码](https://github.com/worldbench/SCOPE) · [数据](https://huggingface.co/datasets/worldbench/MIST-Bench)

2. **[Routing Is Least Learnable Where It Is Most Valuable: Bounds on Representation Routing for Web Agents](./routing-representation-for-web-agents.md)**  
   **Spotlight：** 论文在真实 web-agent 噪声下澄清了 routing 的真实上限：最有价值的路由场景往往最难学习，重复误差是关键干扰。
   [论文](https://arxiv.org/abs/2608.06171) · [PDF](https://arxiv.org/pdf/2608.06171)

3. **[Causal Episodic Memory for Feedback-Driven Agent Repair](./causal-episodic-memory-agent-repair.md)**  
   **Spotlight：** MERIT 探索“无参数”记忆复用，证明 Text-to-SQL 场景下可带来稳定但受限的增益，适合做 agent 修复系统的成本友好增强。
   [论文](https://arxiv.org/abs/2608.05906) · [PDF](https://arxiv.org/pdf/2608.05906)

4. **[MASS: Multiplayer World Models with Authoritative Shared State](./mass-multiplayer-world-models.md)**  
   **Spotlight：** 将多人世界建模拆成共享状态推进与视角渲染两步，支持高并发下的一致模拟与扩展，给具身智能提供结构化 baseline。
   [论文](https://arxiv.org/abs/2608.06257) · [PDF](https://arxiv.org/pdf/2608.06257) · [项目页](https://alaya-lab.github.io/MASS/)

5. **[MetaboLLM: a metabolomics-specialized large language model for biochemical knowledge integration and predictive metabolite graph construction](./metabollm-metabolomics-llm.md)**  
   **Spotlight：** 在 metabolomics 场景中把知识库对齐、LLM 适配与图神经预测打通，形成兼顾性能与解释性的 AI4S 端到端路径。
   [论文](https://arxiv.org/abs/2608.06253) · [PDF](https://arxiv.org/pdf/2608.06253)

## 阅读提示

- **先读 SCOPE + Routing**：可快速建立“何时信任上下文、何时信任视觉/文本表示”的统一思路。
- **再读 MERIT**：关注反馈驱动 agent 的记忆机制与“收益-成本”边界。
- **关注 MASS 与 MetaboLLM**：前者偏具身仿真，可观测性强；后者偏 AI4S，可解释性强。
