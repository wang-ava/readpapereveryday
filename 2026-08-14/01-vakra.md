# VAKRA: Evaluating Multi-Hop Reasoning Across APIs and Retrieval Under Tool-Use Policies

> Spotlight：VAKRA 把企业工具化 Agent 的“调用 API + 检索 + 工具策略约束”放进同一套可执行 benchmark，结果显示瓶颈不在 API 调用本身，而是多跳语言归因与跨源推理。

- 论文标题：VAKRA: Evaluating Multi-Hop Reasoning Across APIs and Retrieval Under Tool-Use Policies
- 作者（机构）：Ankita Rajaram Naik, Anupama Murthi, Benjamin Elder, Siyu Huo, Raavi Gupta, Abhinav Jain, Praveen Venkateswaran, Abdulhamid Adebayo, Danish Contractor；机构未在 arXiv 页面直接给出（可通过作者主页/机构主页进一步确认）
- 发布日期（版本日期）：2026-08-12（arXiv v1）
- 主题标签：`#Agent` `#ToolUse` `#API` `#Retrieval` `#Benchmark`
- 论文链接：[https://arxiv.org/abs/2608.12282](https://arxiv.org/abs/2608.12282)
- PDF 链接：[https://arxiv.org/pdf/2608.12282v1](https://arxiv.org/pdf/2608.12282v1)
- 项目/代码/数据链接（如可得）：GitHub [https://github.com/IBM/VAKRA](https://github.com/IBM/VAKRA)、Hugging Face Dataset [https://huggingface.co/datasets/ibm-research/VAKRA](https://huggingface.co/datasets/ibm-research/VAKRA)
- 核心问题：Agent 在真实工作流中经常需同时完成 API 编排和文档检索，并在策略约束下进行多跳推理，但现有 benchmark 常将这些能力分离评估，难以真实反映复合场景表现。
- 方法概要：论文构建了 VAKRA benchmark，覆盖 62 个领域、8000+ 可执行 API，设置三档递增难度：多样化 API 交互、基于 API 的多跳推理、含自然语言策略约束的多源推理。评测采用固定 ReAct harness 与 live API 重放执行，允许多个有效调用路径，提高评测公平性与可复现实验性。
- 主要贡献：
  - 首次公开大规模兼具 API 与检索任务的多跳 Agent benchmark。
  - 强调“策略约束”维度（policy-aware）并将其并入标准化评测流程。
  - 给出可执行链路验证方法，减少 benchmark 中“形式正确但语义错误路径”的偏差。
- 关键实验或结果：在 frontier 与开源模型上的评测中，单跳 endpoint 任务中最好模型也只有约 70.4%；组合 API 任务下降到 50%–51%；随着推理深度增加性能下降超过 50%，在 policy-constrained 与不可回答问题上最低可降到约 2.4%。
- 适合关注的原因：能直接揭示企业级 Agent 的真实可用性边界，尤其是语义层归因与跨源 grounding 的系统性瓶颈，对落地自动化流程很有指导意义。
- 局限性或待验证点：结果基于当前 62 领域的 API 采样分布，可能对外部行业场景外推有限；策略模板较集中，复杂组织协作（multi-agent 协同）能力尚未覆盖。
- 对后续研究/应用的启发：后续可聚焦“语言层 disambiguation 与 source-grounding”模块增强，结合 retrieval planning 与 API schema-aware policy，提升 Agent 在长链路任务中的鲁棒性。
- 适合 Obsidian 快速浏览的中文总结：VAKRA 显示多跳 Tool-Use 的真实难点在语言推理和策略执行耦合，单纯调用 API 能力并不足以应对复杂企业任务。

## 标准化研究框架

**Research question：** 在有策略约束的企业场景中，LLM Agent 能否在多跳 API 调用与检索场景下保持可复现、可解释的推理性能？

**Literature：** 现有工作常分别评估 tool use 或 retrieval，缺少把 API 与检索统一建模为多跳链路的 benchmark。VAKRA 处于对 Agent 基准体系从“单点能力”走向“完整行为链”评估的关键过渡。

**Theory：** 当智能体需在真实系统中决策调用时，正确性不只取决于单步调用是否可执行，更依赖语义状态更新与策略一致性。该问题可视为“结构化动作空间 + 语言推理 + 外部约束”的三重约束规划。

**Hypotheses：** 多跳深度越高，性能下降越明显；不同模型差距会在 policy-constrained 条件下放大；语言中介层失误是主导误差来源之一。

**Method：** 构建跨领域 API 集合与任务模板；设定三层任务难度；通过固定 ReAct harness 运行模型输出；使用 live API 重执行校验成功性并统计正确率曲线与深度敏感性。

**Data and Analysis：** 数据量约 8,000+ API、62 领域，按任务类型分层采样。分析维度包括单跳/多跳成功率、不可回答问题下误报率、策略约束下的成功衰减，以及调用路径追踪的 failure analysis。

**Findings：** 多跳与 compositional setting 明显压制模型性能，策略约束可引发严重塌陷（最低到约 2.4%），说明“能调用不等于能推理”、语义消歧与跨源 grounding 是当前瓶颈。

**Conclusion：** 论文为 Agent 评测建立了更贴近产品化场景的验证基准；后续工作应把语言规划模块与 API 执行器协同训练，提高长链路工具使用的稳定性与可控性。
