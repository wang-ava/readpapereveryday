# ToolPrivacyBench: Benchmarking Purpose-Bound Privacy in Tool-Using LLM Agents

工具调用能力是现代 LLM Agent 的核心能力之一，但当前评测常只看“任务是否完成”与“最终答复是否合规”。这篇论文指出，隐私风险往往发生在多步工具轨迹中，并通过中间调用传递敏感信息而放大，因此需要“目的边界导向（purpose-bound）”的隐私评估。  

论文提出专门 benchmark，聚焦任务流程级别的隐私约束，不仅判断泄露与否，还要判定信息流是否越界，适用于企业内部工具与外部数据源联动的 Agent 场景。

- **论文标题**：ToolPrivacyBench: Benchmarking Purpose-Bound Privacy in Tool-Using LLM Agents
- **作者/机构（如可得）**：Shijing Hu, Liang Liu, Zhu Meng, Zhicheng Zhao（机构未在 arXiv 元数据中完整给出）
- **发布日期或版本日期**：2026-06-26（v1）
- **主题标签**：#LLM #Agent #Privacy #ToolUse #Benchmark
- **论文链接**：<https://arxiv.org/abs/2606.28061v1>
- **PDF 链接**：<https://arxiv.org/pdf/2606.28061v1>
- **项目/代码/数据链接（如可得）**：论文摘要与元数据未直接给出完整代码仓与完整数据下载链接；建议后续关注作者发布页与补充材料

- **核心问题**：
  LLM Agent 在调用工具时的隐私评估通常是静态和最终态的，缺乏对中间过程的目的边界控制。本文要回答：如何度量“何时泄露是可接受的、何时属于越权传播”。

- **方法概要**：
  1. 重新定义 privacy risk：从最终输出迁移到 tool-call trajectory（工具调用轨迹）级别。  
  2. 引入 purpose-bound 隐私概念，按任务目标设定允许的信息流。  
  3. 构建 benchmark 任务集与评分协议，分别覆盖不同工具类型、不同上下文长度及不同隐私敏感级别。  
  4. 对比模型与策略在任务完成率之外的“越界信息传播率”和“目的一致性”指标。  

- **主要贡献**：
  1. 将隐私评估问题从“response-level”提升到“interaction-level”。  
  2. 定义并形式化 purpose-bound 的评测标准，补齐工具型 Agent 安全测试空白。  
  3. 提供可复用的 benchmark 结构，可直接用于企业级 agent 安全评估。  

- **关键实验或结果**：
  - 论文强调了现有方法在“看答案是否安全”层面的盲区，且在多工具链路下隐私风险更容易被掩盖。  
  - 初步实验显示，ToolPrivacyBench 能更细粒度区分“能回答对但泄露不当”和“回答受限但保留目的一致性”的模型行为。  

- **适合关注的原因**：
  1. LLM Agent 的实际部署重点正在从功能正确转向治理就绪（governance-ready），该评测标准与这一趋势直接对齐。  
  2. 对安全、合规、RAG+Tools 工作流有直接指导价值。  
  3. 可用于构建最小权限与工具编排的评测流程，降低上线风险。  

- **局限性或待验证点**：
  1. 基准覆盖是否涵盖所有行业合规场景仍需行业数据补齐。  
  2. 隐私边界的人工标注仍有主观性，标准化边界规则需持续迭代。  
  3. 真实生产系统中的日志缺失和异步工具链路可能影响指标稳定性。  

- **对后续研究/应用的启发**：
  可将该基准用于“Agent policy 排查 + 工具白名单 + 责任追踪”三位一体的治理栈，特别适合搭配自动化审计系统实现预上线门禁。  

- **一句适合 Obsidian 快速浏览的中文总结**：ToolPrivacyBench 把 agent 安全从最终答案正确率扩展到过程隐私边界控制，适合用于真实工具编排系统的上线前验收。  

## 标准化研究框架
- **Research question：** 在 tool-using LLM Agent 场景里，如何量化“目的边界内”的信息共享与越界隐私泄露？  
- **Literature：** 与传统隐私 benchmark 只评估最终输出相比，本文加入多步交互过程并强调工具调用序列，这是对安全评测文献的重要补充。  
- **Theory：** 本文理论上等价于在 Agent MDP 中定义额外的隐私状态约束，使策略必须满足 task-goal 与 privacy-goal 的双重可行性。  
- **Hypotheses：** 如果评估指标同时覆盖轨迹和目的边界，模型选择与策略调优将更能反映真实部署安全性。  
- **Method：** 设计多场景 benchmark，比较不同模型在任务完成率与隐私合规性上的 trade-off。  
- **Data and Analysis：** 由论文构建任务集与注释标准，并在多模型/多场景下统计 purpose-bound 违例率、敏感信息传播长度和任务成功率。  
- **Findings：** 结果显示，仅看最终输出不足以识别重要风险；轨迹级隐私评估可暴露更多越权行为。  
- **Conclusion：** 在本文语境下该框架是安全治理工具，不是纯精度 benchmark；对工程团队的价值在于构建可量化的隐私上线门槛。
