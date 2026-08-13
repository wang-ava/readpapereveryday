# EvoHarness-RL: Learning Self-Evolving Runtime Harness for Long-Horizon LLM Agents

> Spotlight：EvoHarness-RL 把长程 Agent 的外部状态管理问题从提示工程，升级为可训练的策略问题，显示出“让 agent 学会有选择地用状态/工具”比单纯增大模型更有效的趋势。

- 论文标题：EvoHarness-RL: Learning Self-Evolving Runtime Harness for Long-Horizon LLM Agents
- 作者（机构）：Xuying Ning, Dongqi Fu, Tianxin Wei, Hanqing Zeng, Yuanchen Bei, Bingxuan Li, Zihao Li, Qifan Wang, Xiang Shen, Yifan Wu, Jiayi Liu, Hong Li, Yinglong Xia, Xiangjun Fan, Hanghang Tong, Jingrui He；机构未在页面统一给出（需通过论文附录或机构主页确认）
- 发布日期（版本日期）：2026-08-05（arXiv v1，Submission: Wed, 5 Aug 2026）
- 主题标签：`#LLMAgent` `#ToolUse` `#ReinforcementLearning` `#LongHorizon`
- 论文链接：[https://arxiv.org/abs/2608.05446](https://arxiv.org/abs/2608.05446)
- PDF 链接：[https://arxiv.org/pdf/2608.05446v1](https://arxiv.org/pdf/2608.05446v1)
- 项目/代码/数据链接（如可得）：论文正文显示“Accepted to LLA@COLM 2026”；未见公开代码/数据链接。
- 核心问题：长时程 LLM Agent 常依赖手工设计的外部 harness/state，但这种硬编码规则难覆盖多任务演进场景。
- 方法概要：定义 Belief/Progress/Experience（BPE）外部状态框架；用监督微调学会 harness 行为，再用 cost-aware GRPO 优化运行期的 state 读取、更新与整合策略。
- 主要贡献：
  - 将 harness policy 作为可训练对象，并与主模型联合优化。
  - 提出 harness 演进机制：训练后自动形成“选择性 harness 调用”而非频繁调用。
  - 强化长链路任务中的外部记忆维护能力。
- 关键实验或结果：在 ALFWorld 上使用 Qwen3-8B，成功率达 96.9%。观察到“harness annealing”与“harness evolution”两个稳定现象。
- 适合关注的原因：长期任务里“该不该调用外部状态、如何更新状态”是核心瓶颈，这篇把行为决策内化进策略本身，利于工程化自动化。
- 局限性或待验证点：主要实验在 ALFWorld，一线 web agent/工具链任务的鲁棒性仍待验证；公开训练代码与超参缺失影响复现。
- 对后续研究/应用的启发：可作为工具调用、任务规划、RAG 检索等系统的统一状态编排器设计起点。
- 适合 Obsidian 快速浏览的中文总结：这项工作证明把 harness 管理训练化后，LLM Agent 在长程任务上可更稳、更少冗余地调用外部状态。

## 标准化研究框架

**Research question：** Agent 能否通过训练学习如何管理和选择性使用外部运行时状态，从而提升长时程执行成功率？

**Literature：** 传统方法多停留在提示词模板和手工规则；本工作把 harness policy 纳入训练流程，与长时程工具使用研究形成衔接。

**Theory：** 外部状态与任务推进之间存在可学习的控制关系，正确的状态管理可减少无效调用，降低噪声和计算浪费。

**Hypotheses：** 引入 BPE 表示并用 GRPO 优化后，agent 在长程任务上的成功率和状态使用效率将提升。

**Method：** 先监督微调学习 harness action space 与状态构建，再以 cost-aware GRPO 做在线策略优化，结合 selective read/update/commit。

**Data and Analysis：** 在 ALFWorld 上评测成功率、调用频率、状态演进模式，观察行为动态是否出现 annealing 与进化趋势。

**Findings：** 成功率达 96.9%，并观察到调用频率下降且状态更紧凑，说明策略对外部状态形成了有用压缩与分层表示。

**Conclusion：** 本研究给出“外部状态可学习化”证据，但其在更复杂开放环境中的泛化需进一步通过公开 benchmark 与复现代码检验。
