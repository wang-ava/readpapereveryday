# When Agents Do Not Stop: Uncovering Infinite Agentic Loops in LLM Agents

## Spotlight（今日速读）
这篇论文抓住了生产系统里最危险却常被忽略的问题：agent 卡死循环与未受控自触发。  
它把“无限重试”从直觉问题变成可静态检测的问题，给工程侧提供了可落地的审核与告警入口。

## 论文标题
When Agents Do Not Stop: Uncovering Infinite Agentic Loops in LLM Agents

## 作者/机构
- 作者：Xinyi Hou, Shenao Wang, Yanjie Zhao, Haoyu Wang
- 机构：arXiv 元数据未给出完整机构；可通过作者主页后续补齐

## 发布日期
2026-07-02（v1）

## 主题标签
#Agent #Safety #StaticAnalysis #LLM #SoftwareEngineering

## 论文链接
https://arxiv.org/abs/2607.01641

## PDF 链接
https://arxiv.org/pdf/2607.01641v1

## 项目/代码/数据链接
- 论文代码/工具仓库：论文摘要未给出固定公开 URL（可在后续更新中补充）
- 数据：作者在 6,549 个 LLM agent 仓库上做规模评估（结果由论文公开）

## 核心问题
当 LLM agent 在迭代式规划、工具调用、状态更新或 agent handoff 中出现反馈路径放大时，会否形成无法停止的循环？如何在不执行代码的前提下提前发现这些闭环并减少成本与安全风险？

## 方法概要
- 构建 IAL-Scan 静态分析框架，输入真实 agent 项目代码。
- 将异构 agent 框架抽象为通用 Agent IR。
- 构建 Agentic Loop Dependence Graph（ALDG），显式恢复 framework-induced 反馈路径和状态扩展路径。
- 检测“可重复到达高成本/状态增长操作”的循环并判断是否存在终止缺失。

## 主要贡献
- 将 agent 失控行为系统化为可检测的控制流问题，而非单靠运行时日志人工排查。
- 提供跨框架可复用的抽象（Agent IR）与反馈闭环模型（ALDG）。
- 在大规模真实仓库上给出可复验的精度基线与误报风险边界。

## 关键实验或结果
- 在 6,549 个 LLM agent 仓库上运行 IAL-Scan，报告 74 个潜在 finding。
- 人工复核确认 68 个高置信度 IAL 失败，覆盖 47 个项目，精度约 91.9%。
- 论文强调在实践中该类问题可导致 context 膨胀、持续调用成本、外部副作用放大等高风险后果。

## 适合关注的原因
这篇工作直接对应 Agentic 系统的可运维性（agentic operability）问题：比“准确率”更接近真实生产需求——止损、可控、可解释。对企业接入 LLM agent 的安全边界建设有明确参考价值。

## 局限性或待验证点
- 论文基于静态分析对运行时语义有一定理想化假设，复杂异步/外部副作用场景可能有边界漏检。
- 对于非主流框架或重度动态反射/元编程代码的建模准确性仍需更多验证。
- 尚未看到对“误报如何与 CI/CD 流程闭环自动抑制”提供完整的工程 recipe。

## 对后续研究/应用的启发
- 建议将 IAL-Scan 融入 pre-merge CI，作为高风险 agent 改动的 gating 检查。
- 可扩展为“终止可验证规范”：结合成本约束（调用预算、文件写入权限、外部 API 次数）进行多目标安全分析。
- 可与 AgentLens 之类的 trajectory 评测结合，形成“静态防线 + 运行时轨迹验证”的双保险。

## 标准化研究框架
- **Research question：** 在真实 agent 代码中，能否静态发现高概率的“无限执行/无收敛”闭环，并将其转化为工程可执行风险清单？  
- **Literature：** 该领域尚缺少统一定义的 production-grade 静态规则；本工作弥合了 agent 编排研究与软件工程静态分析的衔接。  
- **Theory：** 对应非社会科学场景可定义为“反馈闭环可达性检验”：在图模型中识别未满足终止条件且可重复触达高成本操作的控制路径。  
- **Hypotheses：** H1：ALDG 可在大规模仓库中稳定识别真实 IAL；H2：多数 IAL 与缺失终止条件和框架语义耦合；H3：静态分析可显著降低线上故障发生率。  
- **Method：** 通过 Agent IR 归一化不同实现框架，再构图推断高风险循环并按语义类别打分。  
- **Data and Analysis：** 样本规模 6,549 个仓库；输出候选 loop 的报告集（74 条）并人工复核确认（68 条）；对比不同仓库类型与框架路径。  
- **Findings：** 该静态框架在复核层面表现出高精度（91.9%）的候选检出效果，提示循环问题在真实项目中并非边角案例。  
- **Conclusion：** 在 agent 落地阶段，静态闭环检测比事后监控更具成本优势，应作为 LLM agent 安全治理的第一道防线。  

一句话总结：把 agent 的“不会停”变成可定义、可检测、可治理的循环问题，是迈向可控 agent 系统的关键步骤。
