# Recursive Experiential-Working Memory Evolution for Long-Horizon Agent Harnesses

该文提出可自我进化的 Agent harness 框架：通过工作记忆与经验记忆的协同，让代理在长时任务中持续修复决策策略。

## 论文标题
Recursive Experiential-Working Memory Evolution for Long-Horizon Agent Harnesses

## 作者/机构
- 作者：Zhaochen Yu, Yingcheng Wu, Zhenfei Yin, Kaiyuan Chen, Zhe Zhao, Mengdi Wang, Shuicheng Yan, Ling Yang
- 机构：arXiv 摘要页未显式列出

## 发布日期/版本日期
- 提交日期：2026-08-25（v1）
- 版本日期：2026-08-25

## 主题标签
#Agent #LLM #LongHorizon #Memory #SelfImprovement

## 论文链接
- https://arxiv.org/abs/2608.24876

## PDF 链接
- https://arxiv.org/pdf/2608.24876v1

## 项目/代码/数据链接
- 代码： https://github.com/Gen-Verse/Recuris
- 数据：未在摘要页公开给出

## 核心问题
面对长时、多步的 agent 任务，历史上下文越长，任务状态越模糊，导致技能选择失准与失败难以定位；本文问的是如何让 agent harness 自动识别并纠偏这些失败。

## 方法概要
- 将长期执行过程拆分为**工作记忆（Working Memory）**与**经验记忆（Experiential Memory）**：前者跟踪当前任务进度与关键里程碑，后者保存可复用的技能执行片段。
- 由 Working Memory 驱动的策略选择把技能调用约束到当前需求，避免盲目依赖全部历史。
- 执行产生的证据被结构化后交给固定的 Meta-Agent，生成局部、可验证的更新，写回 Skill Memory。
- 形成“执行 -> 证据 -> 验证更新 -> 重新执行”的递归闭环，实现 bounded 的 memory-evolution loop。

## 主要贡献
1. 将长时 agent 的稳定性问题抽象为记忆管理问题，而非单一模型能力问题。
2. 提出工作记忆/经验记忆协同的可迭代机制，支持长期任务中的技能自我修正。
3. 通过固定 Meta-Agent 将错误定位到可行动作层，增强可追踪性和调试性。

## 关键实验或结果
- 在 4 个长时任务基准与 10 个模型上，完成 37/37 对比任务中的 35 个任务成功率提升。
- 对 Tau-bench 的提升：GPT-5.6 Sol +17.8，Claude Opus 5 +15.6，前者后升至 87.9%。
- 在 Qwen3.6-27B/35B 上分别提升 +16.6/+13.5。
- 任务时长增加时收益继续上升（最高场景 +32.2），常见长时失败率可降至 80% 以内。

## 适合关注的原因
它把“代理会变差、失稳、不可复现”这类工程痛点直接接到一个统一机制上，尤其适合关注能否把 agent 从一次性 demo 转为持续迭代系统的研究。

## 局限性或待验证点
- 在真实高噪声线上环境中（API 波动、工具故障、跨域任务）能否稳定收敛尚未明确。
- 该机制的 token/算力开销和缓存策略代价尚未公开完整曲线。
- 公开评测仍偏向基准任务，行业级长周期部署的可靠性仍待检验。

## 对后续研究/应用的启发
- 可将该机制直接映射到企业智能体平台，做“错误可追踪 + 记忆可版本化”的闭环运营。
- 后续可探索与外部验证器结合，建立多智能体/工具生态中的协同 memory-evolution。

## 适合 Obsidian 快速浏览的中文总结
一句话：用可进化记忆把长时 Agent 的历史负担变成结构化学习资源。

## 标准化研究框架
**Research question：** 在长时任务中，如何让代理通过可验证的执行证据自动更新记忆与策略，从而减少控制层失配并提升成功率？

**Literature：** 现有 LLM Agent 工作多集中在 prompt、模型规模或工具调用增强，但对执行轨迹可持续自我修正链路覆盖不足；该文补齐了“状态—行为—更新”闭环。

**Theory：** 采用控制系统视角，认定任务成功关键取决于两类状态表示分离（即时状态与历史经验）及其稳定的更新机制。

**Hypotheses：**
1. 任务状态显式记忆可提高后续技能调用质量。
2. 局部、验证过的更新优于全局回放式修订。
3. 长时任务中，闭环迭代可随 horizon 增长保持收益增长。

**Method：** 从 arXiv 摘要可见，本文采用了基于 memory-evolution 的架构设计并在标准长时 benchmark 上做多模型对比，使用固定 Meta-Agent 作为更新控制器。

**Data and Analysis：** 以四类长时基准任务和十个模型结果为数据来源，核心指标为成功率、越界失败率及长时任务增益。

**Findings：** 方法在多个基准与模型上显著提升成功率，并对长时区间有更强收益。

**Conclusion：** 在长时 Agent 研究中，记忆更新与执行可验证性是决定上限表现的核心变量，值得作为平台级设计接口。
